<script setup lang="ts">
import { ref } from 'vue'

const isAuthenticated = ref(false)
const username = ref('')
const password = ref('')
const errorMessage = ref('')

const listaProductos = [
  { id: 101, nombre: 'Teclado Mecánico RGB', precio: 250, stock: 12 },
  { id: 102, nombre: 'Mouse Óptico Inalámbrico', precio: 110, stock: 20 },
  { id: 103, nombre: 'Monitor Gamer 24" 144Hz', precio: 1490, stock: 5 }
]

const handleLogin = () => {
  if (username.value === 'felix.maldonado' && password.value === '1234') {
    isAuthenticated.value = true
    errorMessage.value = ''
  } else {
    errorMessage.value = 'Credenciales incorrectas'
  }
}

const handleLogout = () => {
  isAuthenticated.value = false
  username.value = ''
  password.value = ''
}
</script>

<template>
  <div style="font-family: Arial; padding: 20px; background: #f5f5f5; min-height: 100vh;">
   
    <!-- Login -->
    <div v-if="!isAuthenticated" style="max-width: 350px; margin: 50px auto; background: white; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
      <div style="background: #1a1a1a; color: white; padding: 15px; text-align: center; font-weight: bold;">
        🔒 Sistema de Gestión - ITPM
      </div>
      <div style="padding: 30px;">
        <div style="margin-bottom: 15px;">
          <label style="display: block; font-weight: bold; margin-bottom: 5px;">Usuario Docente</label>
          <input v-model="username" placeholder="Ej: felix.maldonado" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;" />
        </div>
        <div style="margin-bottom: 20px;">
          <label style="display: block; font-weight: bold; margin-bottom: 5px;">Contraseña</label>
          <input v-model="password" type="password" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px;" />
        </div>
        <button @click="handleLogin" style="width: 100%; padding: 10px; background: #2563eb; color: white; border: none; border-radius: 4px; font-weight: bold; cursor: pointer;">
          Ingresar al Sistema
        </button>
        <p v-if="errorMessage" style="color: red; text-align: center; margin-top: 10px;">{{ errorMessage }}</p>
        <p style="margin-top: 20px; font-size: 12px;">Docente: felix.maldonado</p>
      </div>
    </div>

    <!-- Panel -->
    <div v-else style="max-width: 600px; margin: 20px auto; background: white; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
      <div style="background: #16a34a; color: white; padding: 15px; display: flex; justify-content: space-between; align-items: center;">
        <span>📦 Panel de Almacén - Activo</span>
        <button @click="handleLogout" style="background: white; color: #16a34a; border: none; padding: 5px 15px; border-radius: 4px; cursor: pointer; font-weight: bold;">Salir</button>
      </div>
      <div style="padding: 30px;">
        <h2 style="color: #16a34a; text-align: center; margin-bottom: 5px;">¡Bienvenido, Lic. Félix Maldonado!</h2>
        <p style="text-align: center; color: #666; font-size: 14px; margin-bottom: 30px;">Control de Inventarios en Tiempo Real</p>
       
        <div v-for="producto in listaProductos" :key="producto.id" style="border-top: 1px solid #eee; padding: 15px 0; display: flex; justify-content: space-between; align-items: center;">
          <div>
            <div style="font-weight: bold;">⚙️ {{ producto.nombre }}</div>
            <div style="font-size: 12px; color: #666;">ID: {{ producto.id }}</div>
          </div>
          <div style="background: #1a1a1a; color: white; padding: 5px 10px; border-radius: 15px; font-size: 12px;">
            Bs. {{ producto.precio }} | Stock: {{ producto.stock }} pzas.
          </div>
        </div>
      </div>
    </div>
  </div>
</template>