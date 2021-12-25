<template>
    <v-app>
        <v-container>
            <v-row>
                <v-col cols="12">
                    <FormStepper />
                </v-col>
            </v-row>
        </v-container>
    </v-app>
</template>

<script>
export default {
    name: 'App',
    components: {
        FormStepper: () => (import('./components/form-stepper.vue'))
    },
};
</script>

<style lang="scss">
    #app {
        padding: 100px 0;
    }
</style>
