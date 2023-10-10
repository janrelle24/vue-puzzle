<template>
    <div class="text-center pt-5">
        <div>
            <label for="file">
                <input type="file"
                    id="file"
                    accept="image/gif, image/jpeg, image/png"
                >
            </label>
        </div>
        <div class="pt-5">
            <input type="radio" name="level" id="easy" :value="3" v-model="level" checked/>
            <label class="me-4" for="easy">
                Easy
            </label>
        
            <input type="radio" name="level" id="medium" :value="4" v-model="level"/>
            <label class="me-4" for="medium">
                Medium
            </label>
        
            <input type="radio" name="level" id="hard" :value="5" v-model="level"/>
            <label class="me-4" for="hard">
                Hard
            </label>
        </div>
        <div>
            <button type="button" class="btn btn-success mt-4" @click="$emit('start-game', this.level)">START</button>
        </div>
    </div>
</template>

<script>

    export default{
        name: "Start",
        data() {
            return{
                image: null,
                level: 3,
            };
        },
    };
</script>

<style>
label {
    font-size: 18px;
}

button {
    padding: 10px 35px !important;
    font-size: 20px !important;
}

input {
    margin-right: 10px !important;
}
</style>