<template>
    <div class="puzzle">
        <div class="row" v-for="row in size" :key="row">
            <div class="cell" v-for="col in size" :key="col">
                <div v-if="puzzle[row - 1][col - 1]" class="piece">
                    <img :src="puzzle[row - 1][col - 1]" :style="pieceStyle(row, col)" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Game",
    props: ["size", "image"],
    data() {
    return {
        puzzle: [],
        pieceSize: 100, // Assuming each piece is a square of 100x100 px
    };
    },
    mounted() {
        this.initializePuzzle();
    },
    methods: {
    initializePuzzle() {
        // Split the image into pieces
        const pieces = this.splitImage();

        // Shuffle the pieces
        this.shuffle(pieces);

        // Create a 2D array representing the puzzle grid
        this.puzzle = [];
        for (let i = 0; i < this.size; i++) {
        this.puzzle.push([]);
        for (let j = 0; j < this.size; j++) {
            this.puzzle[i].push(pieces[i * this.size + j]);
        }
        }
    },
    splitImage() {
        if (!this.image) return [];
        const pieces = [];
        const imageWidth = this.image.width;
        const imageHeight = this.image.height;
        const pieceWidth = imageWidth / this.size;
        const pieceHeight = imageHeight / this.size;

        for (let i = 0; i < this.size; i++) {
            for (let j = 0; j < this.size; j++) {
            const canvas = document.createElement("canvas");
            const ctx = canvas.getContext("2d");
            canvas.width = pieceWidth;
            canvas.height = pieceHeight;

            ctx.drawImage(
                this.image,
                j * pieceWidth,
                i * pieceHeight,
                pieceWidth,
                pieceHeight,
                0,
                0,
                pieceWidth,
                pieceHeight
            );

            pieces.push(canvas.toDataURL());
            }
        }
        return pieces;
    },
    shuffle(array) {
        for (let i = array.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
        }
    },
    pieceStyle(row, col) {
        return {
          transform: `translate(${(col - 1) * this.pieceSize}px, ${(row - 1) * this.pieceSize}px)`,
        };
    },
    },
};
</script>

<style scoped>
.puzzle {
    display: grid;
    grid-template-columns: repeat(var(--size), 1fr);
    grid-gap: 1px;
}

.row {
    display: flex;
}

.cell {
    flex: 1;
}
.piece {
    width: 100%;
    height: 100%;
    overflow: hidden;
}
.piece img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease-in-out;
}
.piece img.active {
    transform: scale(1.05);
}
</style>
