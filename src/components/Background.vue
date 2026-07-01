<script setup>
    import Body from './Body.vue'
</script>
<template>
    <div class="terminal-container min-h-screen p-6">
    <Body />
    </div>
</template>


<style scoped>
.terminal-container {
    background-color: #0a0c10;
    
    background-image: linear-gradient(
    rgba(18, 24, 38, 0) 50%, 
    rgba(0, 0, 0, 0.3) 50%
    );
    background-size: 100% 2px;
    
    position: relative;
    width: 100%;
    overflow: hidden;
}

.terminal-container::before {
    content: " ";
    display: block;
    position: absolute;
    top: 0; left: 0; right: 0; bottom: 0;
    z-index: 5;
    pointer-events: none;

    background: linear-gradient(
    rgba(16, 185, 129, 0) 0%,
    rgba(16, 185, 129, 0.05) 50%,
    rgba(16, 185, 129, 0) 100%
    );
    background-size: 100% 5px; 
    
    animation: multi-scan-scroll 16s linear infinite;
}



@keyframes multi-scan-scroll {
    from {
    background-position: 0 0;
    }
    to {
    background-position: 0 100%;
    }
}
</style>

