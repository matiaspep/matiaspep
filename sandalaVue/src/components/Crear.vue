<template>
    <div class="container mt-2">
        <div class="card">
  <div class="card-header">
    <h5>Crear Producto</h5>
  </div>
  <div class="card-body">
      <form v-on:submit.prevent="agregarRegistro"> <!-- creo la funcion -->
          <div class="row">
              <div class="mb-3 col-6">
                <label for="nombreProducto" class="form-label">Nombre</label>
                <input type="text" required class="form-control" v-model="producto.nombre" id="nombreProducto">
              </div>

            <div class="mb-3 col-6">
              <label for="categoriaProducto" class="form-label">Categoria</label>
              <select class="form-select"  id="categoriaProducto" aria-label="Elige una categoria">
                <option value="1">One</option>
                <option value="2">Two</option>
                <option value="3">Three</option>
              </select>
            </div>
            
            <div class="mb-3 col">
                <label for="stockProducto" class="form-label">Stock</label>
                <input type="number" required class="form-control" v-model="producto.stock" id="stockProducto">
            </div>

            <div class="mb-3 col-6">
                <label for="descripcionProducto" class="form-label">Descripcion</label>
                <input type="text" required class="form-control" v-model="producto.descripcion" id="descripcionProducto">
              </div>

              <div class="mb-3 col-6">
                <label for="precioProducto" class="form-label">Precio</label>
                <input type="number" required class="form-control" v-model="producto.precio" id="precioProducto">
              </div>

          </div>
          <button type="submit" class="btn btn-success m-1">Agregar</button>
          <button type="submit" class="btn btn-warning m-1">Cancelar</button>
    </form>
    
  </div>
</div>
    </div>
</template>

<script>
export default {

    data(){
        return{
            producto:{}

        }
    },
    methods:{
        agregarRegistro(){
            
            console.log(this.producto);

           // var datosEnviar={nombre:this.producto.nombre, id_categorias:this.producto.categoria}
           var datosEnviar={nombre:this.producto.nombre,stock:parseInt(this.producto.stock),
           descripcion:this.producto.descripcion,precio:parseInt(this.producto.precio)}

            fetch('https://desayunoplaceres.com.ar/apiPepu/apiSandala.php?insertar=1',{
                method:"POST",
                body:JSON.stringify(datosEnviar)
            })
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta=>{
                console.log(datosRespuesta);
                window.location.href='#/listar'
            }))

        }
    },

}
</script>