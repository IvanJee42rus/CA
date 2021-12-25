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
            <v-card outlined>
                <v-card-title>Количество вариантов и экспертов</v-card-title>
                <v-card-subtitle>Укажите число вариантов управления и количество экспертов для формирования матриц. Значения должны быть целыми числами больше единицы.</v-card-subtitle>
                <v-card-text>
                    <v-row>
                        <v-col>
                            <v-text-field 
                                v-model="countControl" 
                                label="Количество вариантов управления"
                                :rules="[rules.required, controlAndExpertRules.min]"
                            ></v-text-field>
                        </v-col>
                        <v-col>
                            <v-text-field 
                                v-model="countExpert" 
                                label="Количество экспертов"
                                :rules="[rules.required, controlAndExpertRules.min]"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-card-text>
                <v-card-actions>
                    <v-btn color="primary" @click="setControlsAndExperts()" :disabled="countControl < 2 || countExpert < 2">Продолжить</v-btn>
                </v-card-actions>
            </v-card>
        </v-stepper-content>

        <v-stepper-content step="2">
            <v-card outlined>
                <v-card-text>
                    <v-row>
                        <v-col :key="index" v-for="(control, index) in controls" cols="6">
                            <v-text-field 
                                :v-model="control" 
                                :label="`${index + 1}. Описание варианта управления`"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-card-text>
                <v-card-actions>
                    <v-btn color="primary" @click="setCurrentStep(3)">Продолжить</v-btn>
                    <v-btn text @click="setCurrentStep(1)">Вернуться</v-btn>
                </v-card-actions>
            </v-card>
        </v-stepper-content>

        <v-stepper-content step="3">
            <v-card outlined>
                <v-card-title>Экспертные оценки</v-card-title>
                <v-card-subtitle>Внесите оценки для каждого эксперта. Оценка должна быть целым числом от 0 до 2.</v-card-subtitle>
                <v-card-text :v-if="vector.length > 0">
                    <v-row>
                        <v-col :key="index" v-for="(matrix, index) in vector" cols="6">
                            <v-card outlined>
                                <v-card-title>{{ index + 1 }}. Эксперт</v-card-title>
                                <v-card-text>
                                    <v-row :key="sIndex" v-for="(row, sIndex) in matrix">
                                        <v-col :key="tIndex" v-for="(col, tIndex) in row">
                                            <v-text-field 
                                                v-model="vector[index][sIndex][tIndex]" 
                                                label="Оценка"
                                                :rules="[rules.required, ratingRules.min, ratingRules.max]"
                                            ></v-text-field>
                                        </v-col>
                                    </v-row>
                                </v-card-text>
                            </v-card>                  
                        </v-col>
                    </v-row>
                </v-card-text>
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
            countControl: 2,
            countExpert: 2,
            vector: [],
            controls: [],
            rules: {
                required: (value) => (!!value || 'Обязательное поле')
            },
            controlAndExpertRules: {
                min: (value) => (value >= 2 || 'Должно быть больше одного'),
            },
            ratingRules: {
                min: (value) => (value >= 0 || 'Минимальная оценка - 0'),
                max: (value) => (value <= 2 || 'Максмальная оценка - 2')
            }
        }),
        methods: {
            setCurrentStep(step) {
                if (step < 1 || step > 3) return;
                this.currentStep = step;
            },
            setControlsAndExperts() {
                this.vector = [];
                this.controls = [];

                for (let i = 0; i < this.countControl; i++) {
                    this.controls.push('');
                }

                for (let i = 0; i < this.countExpert; i++) {
                    let matrix = [];
                    for (let j = 0; j < this.countControl; j++) {
                        matrix[j] = [];
                        for (let k = 0; k < this.countControl; k++) {
                            matrix[j][k] = 0;
                        }
                    }
                    this.vector.push(matrix);
                }
                this.setCurrentStep(2);
            },
            calculate() {
                console.log('calc');
            }
        }
    }
</script>

<style lang="scss" scoped>
    
</style>