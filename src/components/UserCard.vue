<template>
    <v-hover
        v-slot="{ hover }"
    >
        <v-card
             :elevation="hover ? 16 : 2"
             :class="{ 'on-hover': hover }"
             class="mx-auto"
             max-width="400"
             height="100"
             outlined
        >
            <v-list-item three-line>
                <v-list-item-avatar
                        tile
                        size="70"
                        color="grey"
                >
                    <img
                         :src="photo"
                         alt="John"
                    >
                </v-list-item-avatar>
                <v-list-item-content>
                    <div class="overline mb-4">
                        Пользователь
                    </div>
                    <v-list-item-title class="headline mb-1">
                        {{ name }}
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-card>
    </v-hover>
</template>

<script>
    export default {
        name: "UserCard",
        props: ['name', 'photo']
    }
</script>

<style scoped>

</style>
