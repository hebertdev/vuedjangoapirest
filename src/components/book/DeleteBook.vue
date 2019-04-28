<template>
	
	<div>
		<h1>titlo : {{this.form.title}} </h1>
		<h3>description: {{this.form.description}} </h3>	
		<button v-on:click="deleteBook" class="btn btn-danger">Eliminar</button>

	</div>


</template>

<script>
	
	import axios from 'axios';
	import swal from 'sweetalert';
	export default {
		data(){
			return {
				bookId: this.$route.params.bookId,
				form: {
					title:'',
					description:'',
				}
			}
		},

		methods:{
			getBook(){
				const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`
				axios.get(path).then((response)=>{
					this.form.title = response.data.title
					this.form.description = response.data.description
				})
				.catch((error)=>{
					console.log(error)
				})
			},
			deleteBook(){
				const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`
				axios.delete(path).then((response)=>{
					location.href = '/books'
				})
				.catch((error)=>{
					alert('xd')
				})

			}
		},

		created(){
			this.getBook()
		},
	}

		
</script>