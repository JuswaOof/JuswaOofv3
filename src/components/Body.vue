<script setup>
    import { ref, onMounted, nextTick } from 'vue'

    const input = ref('')
    const inputRef = ref(null)

    const history = ref([])
    const historyIndex = ref(0)

    const terminal = ref([])

    const commands = [
    { name: '/help', description: 'List available commands' },
    { name: '/about', description: 'Learn more about me' },
    { name: '/projects', description: 'View my projects' },
    { name: '/socials', description: 'Get in touch with me' },
    { name: '/clear', description: 'Clear the terminal output' },
    { name: '/sudo', description: 'Gives root access and run commands as superuser' },
    ]

    const commandMap = {
        '/help': () => [
            {
            type: 'commands',
            commands
            }
        ],

        '/about': () => [
            {
            type: 'text',
            text: "Hi! I'm Joshua Salcedo, a Full Stack Developer specializing in Laravel and Vue."
            }
        ],

        '/projects': () => [
            {
            type: 'links',
            links: [
                {
                label: 'JuswaOof v2',
                url: 'https://juswaoof.github.io/Portfolio-2022/'
                },
                {
                label: 'JuswaOof v1',
                url: 'https://juswaoof.github.io/2020-Portfolio/'
                },
                {
                label: 'PokeStats',
                url: 'https://juswaoof.github.io/PokeStats/'
                }
            ]
            }
        ],

        '/socials': () => [
            {
            type: 'links',
            links: [
                {
                label: 'GitHub',
                url: 'https://github.com/JuswaOof'
                },
                {
                label: 'LinkedIn',
                url: 'https://www.linkedin.com/in/juswaoof'
                },
                {
                label: 'Email',
                url: 'mailto:joshuasalcedo.juswaoof@gmail.com'
                }
            ]
            }
        ],

        '/sudo': () => {
            window.open(
                'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
                '_blank',
                'noopener,noreferrer'
            )
            terminal.value.push({
                type: 'output',
                lines: [
                    {
                        type: 'text',
                        text: 'haha... you got Rick Rolled 😄'
                    }
                ]
            })
            return null
        },

        '/clear': () => {
            terminal.value = []
            return null
        }
    }

    async function executeCommand() {
        const command = input.value.trim()

        // print prompt
        terminal.value.push({
            type: 'command',
            text: command
        })

        // empty input
        if (!command) {
            input.value = ''
            return
        }

        // save history
        if (history.value.at(-1) !== command) {
            history.value.push(command)
        }

        historyIndex.value = history.value.length

        // Easter egg
        if (/^\/sudo(\s|$)/i.test(command)) {
            terminal.value.push({
                type: 'output',
                lines: [
                    {
                        type: 'text',
                        text: 'haha... you got Rick Rolled 😄'
                    }
                ]
            })

            window.open(
                'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
                '_blank'
            )

            input.value = ''
            await nextTick()
            inputRef.value.focus()
            return
        }

        // execute
        const handler = commandMap[command.toLowerCase()]

        if (handler) {
            const result = handler()

        if (result) {
            terminal.value.push({
                type: 'output',
                lines: result
            })
        }
        } else {
            terminal.value.push({
                type: 'output',
                lines: [
                    {
                        type: 'text',
                        text: `Command not found: ${command}`
                    }
                ]
            })
        }

        input.value = ''

        await nextTick()
        inputRef.value.focus()
    }

    function previousCommand() {
        if (historyIndex.value > 0) {
            historyIndex.value--
            input.value = history.value[historyIndex.value]
        }
    }

    function nextCommand() {
        if (historyIndex.value < history.value.length - 1) {
            historyIndex.value++
            input.value = history.value[historyIndex.value]
        } else {
            historyIndex.value = history.value.length
            input.value = ''
        }
    }

    function focusInput() {
        inputRef.value?.focus()
    }

    onMounted(() => {
        focusInput()

        window.addEventListener('focus', focusInput)
    })
</script>

<template>
    <div class="mx-10 text-white font-mono text-sm" @click="focusInput">
        <div
            v-for="(entry, index) in terminal"
            :key="index"
            class=""
        >

            <!-- Previous Prompt -->
            <template v-if="entry.type === 'command'">
                <div class="flex">
                    <span class="text-green-400">joshua@salcedo</span>
                    <span>:</span>
                    <span class="text-blue-500">~</span>
                    <span>$</span>
                    <span class="ml-2">
                        {{ entry.text }}
                    </span>
                </div>
            </template>

            <!-- Output -->
            <template v-else>

                <div
                    v-for="(line, i) in entry.lines"
                    :key="i"
                >

                    <!-- Plain text -->
                    <template v-if="line.type === 'text'">
                    {{ line.text }}
                    </template>

                    <!-- Help -->
                    <template v-else-if="line.type === 'commands'">
                    <div
                        v-for="command in line.commands"
                        :key="command.name"
                    >
                        <span class="font-bold">
                        {{ command.name }}
                        </span>
                        - {{ command.description }}
                    </div>
                    </template>

                    <!-- Links -->
                    <template v-else-if="line.type === 'links'">
                    <div class="flex gap-4 flex-wrap"
                        v-for="link in line.links">
                        <a
                            :key="link.url"
                            :href="link.url"
                            target="_blank"
                            class="text-blue-400 hover:underline"
                            >
                            ● {{ link.label }}
                        </a>
                    </div>
                    </template>
                </div>

            </template>
        </div>

        <!-- Current Prompt -->
        <div class="flex items-center">
            <span class="text-green-400">joshua@salcedo</span>
            <span>:</span>
            <span class="text-blue-500">~</span>
            <span>$</span>

            <input
                ref="inputRef"
                v-model="input"
                class="ml-2 flex-1 bg-transparent outline-none"
                @keyup.enter="executeCommand"
                @keydown.up.prevent="previousCommand"
                @keydown.down.prevent="nextCommand"
                placeholder="Type a command..."
            />
        </div>

    </div>
</template>

<style scoped>
</style>