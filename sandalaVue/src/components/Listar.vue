<template>
<div class="container mt-2">
    <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Nombre</th>
      <th scope="col">Stock</th>
      <th scope="col">Precio</th>
      <th scope="col">Descripcion</th>
      <th scope="col">Categoria</th>
      <th scope="col">Acciones</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="producto in productos" :key="producto.id">
      <th>{{producto.id}}</th>
      <td>{{producto.nombre}}</td>
      <td>{{producto.stock}}</td>
      <td>{{producto.precio}}</td>
      <td>{{producto.descripcion}}</td>
      <td>{{producto.categoria}}</td>
      <td>
        <button type="button" class="btn btn-success m-1">Editar</button> 
        <button type="button" v-on:click="borrarProducto(producto.id)" class="btn btn-danger m-1">Borrar</button>
      </td>
    </tr>
  </tbody>
</table>
</div>
</template>

<script>
export default {
    data(){
        return{
            productos: []
        }
    },
    created: function(){
        this.consultarProductos();

    },
    methods:{   //consulto Base de Datos
        consultarProductos(){
            fetch('https://desayunoplaceres.com.ar/apiPepu/apiSandala.php')
            .then(respuesta=>respuesta.json())//en caso de que llege respuesta
            .then((datosRespuesta)=>{
                console.log(datosRespuesta)
                this.productos=[]
                if(typeof datosRespuesta[0].success==='undefined')
                {
                    this.productos=datosRespuesta;
                }
            })// la forma en la que vamos a mostrar la info
            .catch(console.log)
        },
        borrarProducto(id){
          console.log(id);

          fetch('https://desayunoplaceres.com.ar/apiPepu/apiSandala.php?borrar='+id)
            .then(respuesta=>respuesta.json())//en caso de que llege respuesta
            .then((datosRespuesta)=>{
                console.log(datosRespuesta)
                window.location.href="#/listar"
                
            })// la forma en la que vamos a mostrar la info
            .catch(console.log)
        }

    }

}
</script>