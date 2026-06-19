<script setup lang="ts">
import { ref } from 'vue'

interface Producto {
  id: number
  nombre: string
  precio: number
  stock: number
}

const isAuthenticated = ref(false)
const username = ref('')
const password = ref('')
const errorMessage = ref('')

const listaProductos: Producto[] = [
  { id: 101, nombre: "Teclado Mecánico RGB", precio: 250, stock: 12 },
  { id: 102, nombre: "Mouse Óptico Inalámbrico", precio: 110, stock: 20 },
  { id: 103, nombre: "Monitor Gamer 24' 144Hz", precio: 1450, stock: 5 }
]

const handleLogin = () => {
  if (username.value === 'felix.maldonado' && password.value === 'itpm2026') {
    isAuthenticated.value = true
    errorMessage.value = ''
  } else {
    errorMessage.value = 'Credenciales incorrectas. Intente de nuevo.'
  }
}

const handleLogout = () => {
  isAuthenticated.value = false
  username.value = ''
  password.value = ''
}
</script>

<template>
  <div style="font-family: sans-serif; max-width: 600px; margin: 50px auto;">
    <div v-if="!isAuthenticated">
      <h4>Sistema de Gestión - ITPM</h4>
      <p>Asignatura: DPW-207</p>
      <div>
        <label>Usuario Docente</label>
        <input v-model="username" type="text" placeholder="felix.maldonado" />
      </div>
      <div>
        <label>Contraseña</label>
        <input v-model="password" type="password" placeholder="••••" />
      </div>
      <div v-if="errorMessage" style="color: red;">{{ errorMessage }}</div>
      <button @click="handleLogin">Ingresar al Sistema</button>
    </div>

    <div v-else>
      <h4>Panel de Almacén - Activo</h4>
      <button @click="handleLogout">Salir</button>
      <h5>¡Bienvenido, Lic. Félix Maldonado!</h5>
      <p>Control de Inventarios en Tiempo Real</p>
      <ul>
        <li v-for="p in listaProductos" :key="p.id">
          <strong>{{ p.nombre }}</strong><br>
          ID: {{ p.id }}<br>
          Bs. {{ p.precio }} | Stock: {{ p.stock }} pzas.
        </li>
      </ul>
    </div>
  </div>
</template>
