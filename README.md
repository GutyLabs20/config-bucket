# config-bucket

## comando para lombock
### java -jar lombock....(la versión que tengas)
### para agregar el Openfeign, se agrega una nueva dependencia maven OpenFeign.
### agregar una nueva interfaz con el nombre openfeign.

List<Pizzeria> listar();
Pizzeria obtenerId(Integer id);
void guardar(Pizzeria pizzeria);
void eliminar(Integer id);
void actualizar(Pizzeria pizzeria);

@Override
public List<Cliente> listar() {
	return repository.findAll();
}

@Override
public Cliente obtenerId(Integer id) {
	return repository.findById(id).orElse(null);
}

@Override
public void guardar(Cliente cliente) {
	repository.save(cliente);
}

@Override
public void eliminar(Integer id) {
	repository.deleteById(id);
}

@Override
public void actualizar(Cliente cliente) {
	repository.saveAndFlush(cliente);
}


	@GetMapping("/listar")
	public @ResponseBody List<Pizzeria> listar(){
		return service.listar();
	}

	@GetMapping("/listar/{id}")
	public @ResponseBody Pizzeria obtener(@PathVariable Integer id) {
		return service.obtenerId(id);
	}
	
	@PostMapping("/guardar")
	public  ResponseEntity<Void> guardar(@RequestBody Pizzeria pizzeria) {
		service.guardar(pizzeria);
		return new ResponseEntity<>(HttpStatus.CREATED);
	}
	
	@PutMapping("/actualizar")
	public @ResponseBody void actualizar(@RequestBody Pizzeria pizzeria) {
		service.actualizar(pizzeria);
	}
	
	@DeleteMapping("/eliminar/{id}")
	public @ResponseBody void eliminar(@PathVariable Integer id) {
		service.eliminar(id);
	}



		List<Cliente> listado = feign.listarClientesSeleccionados();
		ClienteAulaFK fk = null;
		AulaDetalle detalle = null;

		
		for (Cliente cliente : listado) {
			
			fk = new ClienteAulaFK();
			fk.setIdCliente(cliente.getIdCliente());
			fk.setIdPizza(1);
			
			detalle = new ClienteDetalle();
			detalle.setFk(fk);	
			
			repositoryClienteDetalle.save(detalle);
		}