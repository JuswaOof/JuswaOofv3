<template>
    <!-- Title -->
    <div class="mx-10 mb-8">
        <div class="flex justify-center mb-8">
            <pre class="title-logo text-sm">

     ██╗ ██████╗ ███████╗██╗  ██╗██╗   ██╗ █████╗     ███████╗ █████╗ ██╗      ██████╗███████╗██████╗  ██████╗ 
     ██║██╔═══██╗██╔════╝██║  ██║██║   ██║██╔══██╗    ██╔════╝██╔══██╗██║     ██╔════╝██╔════╝██╔══██╗██╔═══██╗
     ██║██║   ██║███████╗███████║██║   ██║███████║    ███████╗███████║██║     ██║     █████╗  ██║  ██║██║   ██║
██   ██║██║   ██║╚════██║██╔══██║██║   ██║██╔══██║    ╚════██║██╔══██║██║     ██║     ██╔══╝  ██║  ██║██║   ██║
╚█████╔╝╚██████╔╝███████║██║  ██║╚██████╔╝██║  ██║    ███████║██║  ██║███████╗╚██████╗███████╗██████╔╝╚██████╔╝
 ╚════╝  ╚═════╝ ╚══════╝╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═╝    ╚══════╝╚═╝  ╚═╝╚══════╝ ╚═════╝╚══════╝╚═════╝  ╚═════╝</pre>
        </div>

        <!-- Details -->
        <div class="flex flex-col">
            <p class="font-mono text-white text-sm">
            Welcome to JuswaOof v3.0! This is a terminal-based web app that showcases my skills and projects. You can also use the command line interface to navigate through the website and access different features. 
            If you have any questions or feedback, please don't hesitate to reach out to me using <span class="font-bold text-md italic">'/socials'</span>. Thank you for visiting!</p>
            <p class="font-mono text-white text-sm">
            Type <span class="font-bold text-md italic">'/help'</span> to see a list of available commands.
            </p>
        </div>
    </div>
    
</template>

<style scoped>
    .title-logo {
        font-family: monospace;
        line-height: 1;

        background: linear-gradient(
            180deg,
            #fde68a,
            #fbbf24,
            #fb923c,
            #f97316,
            #ef4444,
            #be123c
        );

        -webkit-background-clip: text;
        background-clip: text;

        -webkit-text-fill-color: transparent;
        color: transparent;

        display: inline-block;
    }
</style>