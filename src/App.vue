<template>
	<div class="corpo">
		<h1 class="centralizado" v-text='title'></h1>
		<!--<h1 v-text='title'></h1>-->

		<ul class="lista-fotos">
			<li v-for="foto of fotos" class="lista-fotos-item">
				<meu-painel :titulo="foto.titulo">
					<img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
				</meu-painel>		
			</li>
		</ul>

		<!--<img v-bind:src=foto.url v-bind:title=foto.titulo>-->
	</div>
</template>

<script>
	import Painel from './components/shared/painel/Painel.vue';

	export default {

		components : {
			'meu-painel' : Painel
		},

		data() {
			return {
				title : 'Dashboard de Imagens',
				fotos : []
			}
		},
		created() {
			this.$http.get("http://localhost:3000/v1/fotos")
			.then(res => res.json())
			.then(fotos => this.fotos = fotos, error => console.log(error));
		}
	}
</script>

<style lang="scss">
	.corpo {
		font-family: Helvetica, sans-serif;
	}

	.centralizado {
		text-align: center;
	}

	.lista-fotos {
		list-style: none;
	}

	.lista-fotos-item {
		display: inline-block;
	}

	.imagem-responsiva {
		width: 100%;
	}
</style>