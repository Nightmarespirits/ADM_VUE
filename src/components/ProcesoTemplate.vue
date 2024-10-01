<template>
    <v-container>  
        <v-breadcrumbs :items="breadcumbItems">
            <template v-slot:prepend>
                <v-icon icon="mdi-home" size="small"></v-icon>
            </template>
        </v-breadcrumbs>
        <h1>Nuevo Proceso</h1>
        <form @submit.prevent="submit">
            <v-container>
                <v-row justify="center">
                    <v-col>
                        <v-sheet class="pa-2 ma-2">
                            <v-select v-model="select.value.value" :error-messages="select.errorMessage.value" :items="items" label="Local" >

                            </v-select>
                        </v-sheet>        
                    </v-col>
                    <v-col>
                        <v-sheet class="pa-2 ma-2">
                            <v-select v-model="select.value.value" :error-messages="select.errorMessage.value" :items="items" label="Responsable" ></v-select>
                        </v-sheet>                   
                    </v-col>
                    <v-col>
                        <v-sheet class="pa-2 ma-2">
                            <v-dialog v-model="dialog_addDetails" transition="dialog-bottom-transition" fullscreen>
                                <template v-slot:activator="{ props: activatorProps }">
                                    <v-btn
                                    prepend-icon="mdi-open-in-new"
                                    v-bind="activatorProps">

                                    Detalles

                                    <template v-slot:append>
                                        <v-icon color="warning"></v-icon>
                                    </template>
                                    </v-btn>
                                    
                                </template>
                                <v-card>
                                    <v-toolbar>
                                    <v-btn
                                        icon="mdi-close"
                                        @click="dialog_addDetails = false"
                                    ></v-btn>

                                    <v-toolbar-title>Agregar Detalles de Proceso Lavado</v-toolbar-title>

                                    <v-spacer></v-spacer>

                                    <v-toolbar-items>
                                        <v-btn
                                        text="Guardar"
                                        variant="text"
                                        @click="dialog_addDetails = false"
                                        ></v-btn>
                                    </v-toolbar-items>
                                    </v-toolbar>
                                    
                                    <v-form>
                                        <v-container>
                                            <v-row>
                                                <v-col>
                                                    <v-text-field label="Numero Orden" v-model="phone.value.value" :counter="10" :error-messages="phone.errorMessage.value"></v-text-field>
                                                </v-col>
                                                <v-col>
                                                    <v-text-field label="Numero Orden" v-model="phone.value.value" :counter="10" :error-messages="phone.errorMessage.value"></v-text-field>
                                                </v-col>
                                                <v-col>
                                                    <v-text-field label="Numero Orden" v-model="phone.value.value" :counter="10" :error-messages="phone.errorMessage.value"></v-text-field>
                                                </v-col>
                                                <v-col>
                                                    <v-text-field label="Numero Orden" v-model="phone.value.value" :counter="10" :error-messages="phone.errorMessage.value"></v-text-field>
                                                </v-col>
                                                <v-col>
                                                    <v-text-field label="Numero Orden" v-model="phone.value.value" :counter="10" :error-messages="phone.errorMessage.value"></v-text-field>
                                                </v-col>
                                            </v-row>
                                        </v-container>
                                    </v-form>
                                    
                                </v-card>
                                    
                            </v-dialog>
                        </v-sheet>
                        
                    </v-col>
                    <v-col class="d-flex justify-center">
                        <v-sheet class="pa-2 ma-2">
                            <v-btn  color="success">
                            Guardar Registro
                        </v-btn>
                        </v-sheet>
                        
                    </v-col>
                </v-row>
            </v-container>
        </form>
        <Table @open-dialog="dialog_addDetails = true"></Table>
    </v-container>
    
</template>
<script setup>
import { ref } from 'vue'
import { useField, useForm } from 'vee-validate'
import Table from './Table.vue';
//Breadcumb
const breadcumbItems = ref([
    {
    title: 'Dashboard',
    disabled: false,
    href: '/',
    },
    {
    title: 'Operaciones',
    disabled: false,
    href: '/operaciones',
    },
    {
    title: 'Lavado',
    disabled: true,
    href: '/lavado',
    }
])

const dialog_addDetails = ref(false)

const { handleSubmit, handleReset } = useForm({
validationSchema: {
    name (value) {
    if (value?.length >= 2) return true

    return 'Name needs to be at least 2 characters.'
    },
    phone (value) {
    if (/^[0-9-]{7,}$/.test(value)) return true

    return 'El Numero de orden debe  ser como minimo 7 digitos'
    },
    email (value) {
    if (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value)) return true

    return 'Must be a valid e-mail.'
    },
    select (value) {
    if (value) return true

    return 'Seleccione Un elemento'
    },
    checkbox (value) {
    if (value === '1') return true

    return 'Must be checked.'
    },
},
})
const name = useField('name')
const phone = useField('phone')
const email = useField('email')
const select = useField('select')
const checkbox = useField('checkbox')

const items = ref([
'Item 1',
'Item 2',
'Item 3',
'Item 4',
])

const submit = handleSubmit(values => {
alert(JSON.stringify(values, null, 2))
})
</script>