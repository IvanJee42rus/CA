<template>
    <v-stepper v-model="currentStep" vertical>
        <v-stepper-step :complete="currentStep > 1" step="1">
            Варианты и эксперты
        </v-stepper-step>

        <v-stepper-step :complete="currentStep > 2" step="2">
            Варианты управления
        </v-stepper-step>

        <v-stepper-step step="3">
            Экспертные оценки
        </v-stepper-step>

        <v-stepper-content step="1">
            <v-card elevation="2" outlined>
                <v-card-title>Количество вариантов и экспертов</v-card-title>
                <v-card-subtitle>Укажите число вариантов управления и количество экспертов для формирования матриц. Значения должны быть целыми числами больше нуля.</v-card-subtitle>
                <v-card-text>
                    <v-row>
                        <v-col>
                            <v-text-field v-model="countControl" label="Количество вариантов управления"></v-text-field>
                        </v-col>
                        <v-col>
                            <v-text-field v-model="countExpert" label="Количество экспертов"></v-text-field>
                        </v-col>
                    </v-row>
                </v-card-text>
                <v-card-actions>
                    <v-btn color="primary" @click="setCurrentStep(2)">Продолжить</v-btn>
                </v-card-actions>
            </v-card>
        </v-stepper-content>

        <v-stepper-content step="2">
            <v-card elevation="2" outlined>
                <v-card-title>Количество вариантов и экспертов</v-card-title>
                <v-card-subtitle>Укажите число вариантов управления и количество экспертов для формирования матриц. Значения должны быть целыми числами больше нуля.</v-card-subtitle>
                <v-card-actions>
                    <v-btn color="primary" @click="setCurrentStep(3)">Продолжить</v-btn>
                    <v-btn text @click="setCurrentStep(1)">Вернуться</v-btn>
                </v-card-actions>
            </v-card>
        </v-stepper-content>

        <v-stepper-content step="3">
            <v-card elevation="2" outlined>
                <v-card-actions>
                    <v-btn color="primary" @click="calculate()">Вычислить</v-btn>
                    <v-btn text @click="setCurrentStep(2)">Вернуться</v-btn>
                </v-card-actions>
            </v-card>
        </v-stepper-content>
    </v-stepper>
</template>

<script>
    export default {
        name: 'FormStepper',
        data: () => ({
            currentStep: 1,
            countControl: 0,
            countExpert: 0
        }),
        methods: {
            setCurrentStep(step) {
                if (step < 1 || step > 3) return;
                this.currentStep = step;
            },
            calculate() {
                console.log('calc');
            }
        }
    }
</script>

<style lang="scss" scoped>
    .v-card {
        padding: 20px;
        margin: 20px 0;
    }
</style>