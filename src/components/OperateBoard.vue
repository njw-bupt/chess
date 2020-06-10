<template>
    <div class='operation'>
        <div>
            <button @click="$emit('restart-game')">Restart</button>
        </div>
        <div>
            <!-- 该用法只限于animate.css@3.5.1版本 -->
            <transition        
                enter-active-class="animated zoomIn"
                leave-active-class="animated zoomOut"
            >
                <p v-if='result=="X"||result=="O"'>{{ result }} is the winner!</p>
                <p v-if='result=="none"'>The game ended in a draw.</p>
            </transition>
        </div>
    </div>
</template>

<script>
export default {
    name: 'OperateBoard',
    props: {
        result: String
    }
}
</script>

<style scoped>
.operation{
    width: 250px;
    display: inline-block;
    /* border: 1px solid black; */
    vertical-align: top;
    margin-left: 10px;
    text-align: center;
}

</style>