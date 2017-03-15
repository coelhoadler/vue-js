<template>
	<div>
		<h1 v-text='title'></h1>
		<!--<h1 v-text='title'></h1>-->

		<ul>
			<li v-for="foto of fotos">
				<img :src="foto.url" :alt="foto.title">
			</li>
		</ul>

		<!--<img v-bind:src=foto.url v-bind:title=foto.titulo>-->
	</div>
</template>

<script>
	export default {
		data() {
			return {
				title : 'Dashboard de Imagens',
				fotos : []
			}
		},
		created() {
			alert("criei o componente")
		}
	}
</script>

<style lang="scss">

</style>