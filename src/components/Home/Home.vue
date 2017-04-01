<template>
	<div>
		<h1 class="centralizado" v-text='title'></h1>
		<!--<h1 v-text='title'></h1>-->

		<input type="search" class="filtro" placeholder="filtre por parte do título" v-on:input="filtro = $event.target.value">

		<ul class="lista-fotos">

          <li class="lista-fotos-item" v-for="foto of fotosComFiltro">

              <meu-painel :titulo="foto.titulo">

                <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>

                <meu-botao rotulo="remover" tipo="button"/>

              </meu-painel>

          </li>
		</ul>
	</div>
</template>

<script>
	import Painel from '../shared/painel/Painel.vue';
	import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
	import Botao from '../shared/botao/Botao.vue';

	export default {

		components : {
			'meu-painel' : Painel,
			'imagem-responsiva' : ImagemResponsiva,
			'meu-botao' : Botao
		},

		data() {
			return {
				title : 'Dashboard de Imagens',
				fotos : [],
				filtro : ''
			}
		},
		created() {
			this.$http.get("http://localhost:3000/v1/fotos")
			.then(res => res.json())
			.then(fotos => this.fotos = fotos, error => console.log(error));
		},

		computed : {
			fotosComFiltro() {
				if (this.filtro) {
					let exp = new RegExp(this.filtro.trim(), 'i');
					return this.fotos.filter(foto => exp.test(foto.titulo));
				} else {
					return this.fotos;
				}
			}

		}
	}
</script>

<style lang="scss">
	.centralizado {
		text-align: center;
	}

	.lista-fotos {
		list-style: none;
	}

	.lista-fotos-item {
		display: inline-block;
	}

	.filtro {
		display: block;
		width: 100%;
	}
</style>