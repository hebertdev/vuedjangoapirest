<template>
	<div class="container">
		<div class="row">
			<div class="col text-left">
				<h2>listado de libros</h2>

				<!-- <div class="col-md-12">
					<b-table striped hover :items="books" :fields="fields">

						<template slot="action" slot-scope="data">

							<b-button size="sm" variant="primary">
								editar
							</b-button>
							<b-button size="sm" variant="danger">
								eliminar
							</b-button>
							
						</template>
					</b-table>
				</div>
 --> 				<router-link :to="'/books/new/' " > crear </router-link>

				<table class="tablita" style="padding:5px" className="lukas">
				  <tr>
				    <th v-for="field in fields">{{field.key}}</th>
				  </tr>
				  <tr v-for="book in books">
				    <td>{{book.title}}</td>
				    <td>{{book.id}}</td>

				    <td>{{book.description}}</td>
				    <td>
				    <!-- <b-button size="sm" variant="primary" :to="{name:'EditBook' , params: {bookId: data.item.id } }">
								editar
							</b-button> -->
							<!-- <template slot="action" slot-scope="data"> -->
								<!-- <router-link to="">Principal</router-link> -->
								<router-link :to="'/books/' + book.id + '/edit/' " > Editar </router-link>
								<!-- <button :to="{name:'EditBook', params:{bookId: data.book.id} }" >xddd</button> -->
								<router-link :to="'/books/' + book.id + '/delete/' " > Eliminar </router-link>
							<!-- </template> -->
						</td>
				  </tr>
				</table>
			</div>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	export default {
		data(){
			return {
				fields: [
					{key: 'title' , label: 'titulo'},
					{key: 'description' , label: 'descripcion'},
					{key: 'action' , label: 'accion'},
				],
				books:[
				]
			}
		},
		methods:{
			getBooks(){
				const path = 'http://localhost:8000/api/v1.0/books/'
				axios.get(path).then((response)=>{
					this.books = response.data
				})
				.catch((error)=>{
					console.log(error)
				})
			}
		},

		created(){
			this.getBooks()
		}

	};
</script>