<template>
	<div>
		<h3>Agregar Tareas</h3>
		<form @submit.prevent="agregar">
			<input type="text" placeholder="Nombre"
			class="form-control mb-2" v-model="nota.nombre">

			<input type="text" placeholder="Descripción"
			class="form-control mb-2" v-model="nota.descripcion">

			<button class="btn btn-primary" type="submit">Agregar</button>
		</form>
	</div>
</template>
<script>
export default{
	data(){
		return {
			notas: [],
			nota: { nombre: '', descripcion: '' }
		}
	},
	methods:{
		agregar(){
			if(this.nota.nombre.trim() === '' || this.nota.descripcion.trim() === ''){
		        alert('Debes completar todos los campos antes de guardar');
		        return;
		    }
			// console.log(this.nota.nombre, this.nota.descripcion);
			
			const params = {
				nombre: this.nota.nombre,
				descripcion: this.nota.descripcion,
			}

			this.nota.nombre = '';
			this.nota.descripcion = '';

			axios.post('/notas', params)
			.then(res => {
				this.notas.push(res.data)
			});
		}
	}
	
}
</script>