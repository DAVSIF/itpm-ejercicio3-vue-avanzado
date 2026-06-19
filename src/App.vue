<script setup lang="ts">
import { ref } from 'vue'

interface Producto {
  id: number
  nombre: string
  precio: number
  stock: number
  imagen: string
}

const isAuthenticated = ref(false)
const username = ref('')
const password = ref('')
const errorMessage = ref('')

const listaProductos: Producto[] = [
  {
    id: 101,
    nombre: 'Teclado Mecánico RGB',
    precio: 250,
    stock: 12,
    imagen: 'https://images.unsplash.com/photo-1511467687858-23d96c32e4ae?auto=format&fit=crop&q=80&w=400'
  },
  {
    id: 102,
    nombre: 'Mouse Óptico Inalámbrico',
    precio: 110,
    stock: 20,
    imagen: 'https://images.unsplash.com/photo-1527814050087-3793815479db?auto=format&fit=crop&q=80&w=400'
  },
  {
    id: 103,
    nombre: 'Monitor Gamer 24\' 144Hz',
    precio: 1450,
    stock: 5,
    imagen: 'https://images.unsplash.com/photo-1527443224154-c4a3942d3acf?auto=format&fit=crop&q=80&w=400'
  }
]

const handleLogin = () => {
  if (username.value === 'felix.maldonado' && password.value === 'itpm2026') {
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
        <p style="margin-top: 20px; font-size: 12px;">Docente: felix.maldonado / itpm2026</p>
      </div>
    </div>

    <!-- Catálogo Visual -->
    <div v-else style="max-width: 900px; margin: 20px auto; background: white; border-radius: 8px; padding: 30px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
      <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
        <h2 style="color: #16a34a; margin: 0;">🚀 Almacén Activo</h2>
        <button @click="handleLogout" style="background: #dc2626; color: white; border: none; padding: 8px 20px; border-radius: 4px; cursor: pointer; font-weight: bold;">Salir</button>
      </div>
      <p style="text-align: center; color: #666; margin-bottom: 30px;">
        Bienvenido, <strong>Lic. Félix Maldonado</strong>. Inventario verificado por TypeScript:
      </p>
     
      <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px;">
        <div v-for="p in listaProductos" :key="p.id" style="border: 1px solid #e5e7eb; border-radius: 8px; overflow: hidden; text-align: center; background: #fafafa;">
          <!-- Aquí está el v-bind :src del ejercicio 3 -->
          <img :src="p.imagen" :alt="p.nombre" style="width: 100%; height: 180px; object-fit: cover;" />
         
          <div style="padding: 15px;">
            <h4 style="margin: 10px 0 5px 0; font-size: 16px;">{{ p.nombre }}</h4>
            <p style="color: #666; font-size: 14px; margin: 5px 0;">ID: {{ p.id }}</p>
           
            <div style="display: flex; justify-content: center; gap: 10px; margin: 15px 0;">
              <span style="background: #16a34a; color: white; padding: 5px 12px; border-radius: 20px; font-size: 14px; font-weight: bold;">
                Bs. {{ p.precio }}
              </span>
              <span style="color: #2563eb; font-weight: bold; font-size: 14px;">
                {{ p.stock }} pzas.
              </span>
            </div>
           
            <button style="width: 100%; padding: 8px; background: white; border: 1px solid #ccc; border-radius: 4px; cursor: pointer;">
              Gestionar Stock
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>