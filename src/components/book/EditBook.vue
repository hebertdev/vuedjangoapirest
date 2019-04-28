<template>
	<div class="container">
		<div class="row">
			<div class="col text-left">
				<h2>Editar libro</h2>
			</div>
		</div>
		<div class="row">
			<div class="col">
				<div class="card">
					<div class="card-body">
						<form @submit="onSubmit">
							<div class="form-group row">
								<label for="title">Titulo</label>
								<div class="col-sm-6">
									<input type="text" placeholder="Titulo" name="title" class="form-control" autocomplete="off" v-model.trim="form.title">
								</div>
							</div>
							<div class="form-group row">
								<label for="description">Description</label>
								<div class="col-sm-6">
									<textarea name="description" id="description" class="form-control" cols="30" rows="10" placeholder="description" v-model.trim="form.description"></textarea>
								</div>
							</div>

							<div>
								<b-button size="sm" variant="primary" type="submit">Editar</b-button>

								<b-button size="sm" variant="danger" :to="{name:'ListBook' }">
									cancelar
								</b-button>
							</div>
						</form>
					</div>
				</div>
				
			</div>
		</div>
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
			onSubmit(evt){
				evt.preventDefault() 

				const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`
				axios.put(path , this.form).then((response)=>{
					this.form.title = response.data.title
					this.form.description = response.data.description
					
					swal('libro actualizado correctamente','','success')
				})
				.catch((error)=>{
					console.log(error)
					alert('error')
				})
			    
			},
			getBook(){
				const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`
				axios.get(path).then((response)=>{
					this.form.title = response.data.title
					this.form.description = response.data.description
				})
				.catch((error)=>{
					console.log(error)
				})
			}
		},

		created(){
			this.getBook()
		},
	}
		
</script>