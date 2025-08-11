<div align="center">
<h1><strong>ღ¸.🌸´`🌸.¸¸ღ - La chica de la capa roja - ღ¸.🌸´`🌸.¸¸ღ</strong></h1>


●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●
<div align="center">
<h2><strong> ⭐Descripcion del juego y sus mecanicas⭐</strong></h2>
</div>
la chica de la capa roja es un juego de plataformas que consta de 2 niveles, donde requeriras pasar por diferentes obstaculos hechos de 5 tipos de diferentes plataformnas entre ellas Fija, Oscilatoria, Muerte Instantanea, Rebote y Temporal, donde tambien deberas recolectar monedas aumentando tu puntaje para asi poder lograr pasar al siguiente nivel, pero cuidado si llegas a caer al vacio o tocar una plataforma de muerte instantanea tendras que reiniciar el nivel a menos de que llegues a los diferentes chekpoints que hoy por el mapa, cosa que no sera tan facil como parece, mantente en las plataformas con vida, recoge las suficientes monedas para elevar tu puntaje y vuelvete digno de llegar a la meta.


●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●
<div align="center">
<h2><strong>⭐Listado de assets empleados⭐</strong></h2>
</div>
<img width="48" height="16" alt="Platform" src="https://github.com/user-attachments/assets/6a64501c-25c0-4ed2-abaf-bbbe1639c176" />
<img width="499" height="499" alt="Moneda" src="https://github.com/user-attachments/assets/acaa1997-ce06-4335-a6c6-de7b00e06151" />
<img width="192" height="32" alt="Hero_006_Idle" src="https://github.com/user-attachments/assets/9182ec6f-06e9-4e9a-996f-3696e6fafe1c" />
<img width="32" height="32" alt="Door" src="https://github.com/user-attachments/assets/f626d6a2-9cd4-4ebe-b6d8-20fff8b09acb" />
<img width="512" height="512" alt="milestone_16257389" src="https://github.com/user-attachments/assets/572ef221-59b4-4346-bf26-c0cb4d93c50f" />

<div align="center">
<h2><strong>⭐Parallax⭐</strong></h2>
</div>
![2111 w026 n002 1125B p1 1125](https://github.com/user-attachments/assets/0bb083ea-1cf8-43aa-8743-5ca613b58b4d)
![2205_w026_n002_1964b_p1_1964](https://github.com/user-attachments/assets/87bc31c0-49f3-4d51-ae25-efedcc39e6f9)

●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●
<div align="center">
<h2><strong>⭐Descripcion de los codigos empleados para el funcionamiento⭐</strong></h2>
</div>

### 🦋moneda.gd
**-** Este script está diseñado para un nodo Area2D que representa una moneda u objeto recolectable en un juego. Su función principal es detectar cuándo el jugador (que pertenece al grupo "jugador") entra en contacto con esta área. Al hacerlo:

  🔴 Emite una señal personalizada llamada moneda_recolectada, que puede ser utilizada por otros nodos para saber que una moneda fue recolectada.  
  🔴 Se elimina a sí mismo del juego (queue_free()), simulando que la moneda fue recogida.  

**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**
```
extends Area2D  # Este script se aplica a un nodo tipo Area2D en este caso una moneda
signal moneda_recolectada  # Declara una señal personalizada llamada "moneda_recolectada"

func _ready():
	connect("body_entered", Callable(self, "_on_body_entered"))  # Conecta la señal "body_entered" al método "_on_body_entered"
	
func _on_body_entered(body):
	if body.is_in_group("jugador"):  # Verifica si el cuerpo que entró es el jugador
		emit_signal("moneda_recolectada")  # Emite la señal "moneda_recolectada" para notificar que se recogió la moneda
		queue_free()  # Elimina este nodo de la escena (la moneda desaparece)

```
**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**


■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■



### 🦋nivel_0.gd **y** nivel_1.gd
**-** Este script se aplica a un nodo Node2D, que probablemente representa un nivel completo (Nivel0, Nivel1, etc.). Su función principal es:

  🔴 Inicializar un contador de puntos (puntos = 0).  
  🔴 Detectar cuándo una moneda (que pertenece al grupo "moneda") es recolectada, conectando su señal moneda_recolectada.  
  🔴 Actualizar el marcador en pantalla (PuntosLabel) al sumar 200 puntos cada vez que se recolecta una moneda.  
  🔴 Proveer acceso al puntaje actual mediante la función obtener_puntos().  
  

**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**
```

var puntos = 0  # Variable para almacenar la puntuación actual
@onready var puntos_label = $UI/PuntosLabel  # Referencia al Label que muestra los puntos en la UI

func _ready():
	# Por cada nodo en el grupo "moneda", conecta su señal "moneda_recolectada" con la función _on_moneda_recolectada
	for moneda in get_tree().get_nodes_in_group("moneda"):
		moneda.connect("moneda_recolectada", Callable(self, "_on_moneda_recolectada"))
		
func _on_moneda_recolectada():
	puntos += 200  # Suma 200 puntos cada vez que se recoja una moneda
	puntos_label.text = "Puntos: %d" % puntos  # Actualiza el texto del label con el puntaje actual

func obtener_puntos():
	return puntos  # Función que devuelve la cantidad actual de puntos

func _on_checkpoint_body_entered(body: Node2D) -> void:
	pass  # Aquí puedes agregar código para que el checkpoint haga algo cuando el jugador entre
```
**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**

■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■



### 🦋personaje.gd
**-** Este script pertenece a un nodo CharacterBody2D, que representa al jugador principal. Se encarga de su movimiento, salto, gravedad, interacción con zonas de reseteo y puertas, así como de mostrar mensajes en pantalla. Funciona en varios niveles (nivel0, nivel1, etc.).

Sus funciones principales son:  
🔴 Mover al jugador horizontalmente y permitirle saltar.  
🔴 Aplicar gravedad cuando no está en el suelo.  
🔴 Reiniciar el nivel si entra en una zona de reseteo.  
🔴 Cambiar de nivel al llegar a una puerta si tiene al menos 1000 puntos.  
🔴 Mostrar mensajes temporales si no cumple con los requisitos para avanzar o si no hay más niveles.  


**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**
```
extends CharacterBody2D

var velocidad = 200                         # Velocidad horizontal del jugador
var brinco = -400                          # Fuerza del salto (valor negativo para ir hacia arriba)
var gravedad = 1000                        # Fuerza de gravedad que afecta al jugador
@onready var mensaje_label = $MensajeLabel # Referencia al Label para mostrar mensajes en pantalla

var save_path := "user://savegame.json"   # Ruta del archivo donde se guardará la partida

func _ready():
	add_to_group("jugador")                 # Añade el jugador al grupo "jugador" para identificarlo fácilmente

func _physics_process(delta):
	var direccion = Input.get_axis("ui_left", "ui_right")  # Detecta movimiento horizontal del jugador
	velocity.x = direccion * velocidad                     # Aplica velocidad horizontal
	
	if not is_on_floor():
		velocity.y += gravedad * delta                      # Aplica gravedad si está en el aire
	
	if Input.is_action_just_pressed("ui_up") and is_on_floor():
		velocity.y = brinco                                 # Hace que el jugador salte si está en el suelo
	
	move_and_slide()                                        # Aplica movimiento físico

	# Guardar con tecla G
	if Input.is_action_just_pressed("guardar"):
		save_game()                                        # Guarda la partida
		mostrar_mensaje("Juego guardado")                  # Muestra mensaje de confirmación

	# Cargar con tecla C
	if Input.is_action_just_pressed("cargar"):
		load_game()                                        # Carga la partida guardada
		mostrar_mensaje("Juego cargado")                   # Muestra mensaje de confirmación

# --- Guardar posición global y escena ---
func save_game():
	var data := {
		"x": global_position.x,                           # Guarda la posición global X del jugador
		"y": global_position.y,                           # Guarda la posición global Y del jugador
		"scene": get_tree().current_scene.scene_file_path # Guarda la ruta de la escena actual
	}
	var file := FileAccess.open(save_path, FileAccess.WRITE)  # Abre el archivo para escribir
	file.store_string(JSON.stringify(data))                    # Guarda los datos en formato JSON
	file.close()                                               # Cierra el archivo

# --- Cargar posición global y escena ---
func load_game():
	if FileAccess.file_exists(save_path):                      # Verifica que el archivo exista
		var file := FileAccess.open(save_path, FileAccess.READ) # Abre el archivo para leer
		var content := file.get_as_text()                        # Lee el contenido
		file.close()                                             # Cierra el archivo

		var result = JSON.parse_string(content)                  # Convierte JSON a diccionario
		if typeof(result) == TYPE_DICTIONARY:
			if result.has("scene") and result["scene"] != get_tree().current_scene.scene_file_path:
				get_tree().change_scene_to_file(result["scene"]) # Cambia la escena si es diferente
				await get_tree().process_frame                   # Espera un frame para cargar bien
			global_position = Vector2(result["x"], result["y"])   # Posiciona al jugador donde guardó

# --- Cuando muere o cae ---
func _on_reset_area_body_entered(body: Node2D) -> void:
	if body.is_in_group("jugador"):
		load_game()                                             # Reaparece en el último checkpoint guardado

# --- Puerta de cambio de nivel ---
func _on_door_body_entered(body: Node2D) -> void:
	if get_parent().has_method("obtener_puntos"):
		var puntos_actuales = get_parent().obtener_puntos()     # Obtiene puntos del nivel actual

		if puntos_actuales >= 1000:
			var ruta = get_tree().current_scene.scene_file_path
			match ruta:
				"res://nivel0.tscn":
					get_tree().change_scene_to_file("res://nivel1.tscn") # Cambia al siguiente nivel
				"res://nivel1.tscn":
					get_tree().change_scene_to_file("res://nivel2.tscn") # Cambia al siguiente nivel
				_:
					mostrar_mensaje("No hay escena configurada para continuar.") # Mensaje si no hay siguiente nivel
		else:
			mostrar_mensaje("No tienes el suficiente puntuaje de 1000 para pasar de nivel") # Mensaje si falta puntaje
			
func mostrar_mensaje(texto):
	mensaje_label.text = texto                                # Coloca texto en el Label
	mensaje_label.visible = true                              # Hace visible el Label
	await get_tree().create_timer(2.0).timeout                # Espera 2 segundos
	mensaje_label.visible = false                             # Oculta el Label

```
**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**

■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■■━■━■━■

### 🦋plataforma.gd
**-** Este script pertenece a un nodo Area2D que actúa como una plataforma interactiva en el juego. La plataforma puede tener distintos comportamientos dependiendo del tipo que se le asigne por medio de un enum (enumeración).

Los tipos de plataforma definidos son:  
🔴 FIJA: No hace nada especial.  
🔴 OSCILATORIA: Se mueve horizontalmente de forma continua.  
🔴 FRÁGIL: Se destruye 0.5 segundos después de que el jugador la pisa.  
🔴 REBOTE: Hace rebotar al jugador con una fuerza multiplicada.  
🔴 MUERTE: Reinicia el nivel si el jugador la toca.  


**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**
```
extends Area2D  # Este script se aplica a una plataforma basada en Area2D

enum TipoPlataforma {FIJA, OSCILATORIA, FRAGIL, REBOTE, MUERTE}  # Define tipos de plataformas
@export var tipo: TipoPlataforma = TipoPlataforma.FIJA           # Variable exportada para elegir tipo en el editor
@export var fuerza_rebote := 2.0                                # Fuerza de rebote para plataformas REBOTE

func _ready():
	actualizar_plataforma()                                       # Aplica el color y comportamiento según el tipo
	monitorable = true                                            # Permite que este nodo sea detectado por Areas/PhysicsBodies
	monitoring = true                                             # Permite que este nodo detecte colisiones

func actualizar_plataforma():
	match tipo:
		TipoPlataforma.FIJA:
			$Sprite2D.modulate = Color.GREEN                        # Plataforma fija: verde
		TipoPlataforma.OSCILATORIA:
			$Sprite2D.modulate = Color.BLUE                         # Plataforma oscilatoria: azul
			oscilar()                                               # Inicia el movimiento oscilante
		TipoPlataforma.FRAGIL:
			$Sprite2D.modulate = Color.RED                          # Plataforma frágil: roja
		TipoPlataforma.REBOTE:
			$Sprite2D.modulate = Color.YELLOW                       # Plataforma rebote: amarilla
		TipoPlataforma.MUERTE:
			$Sprite2D.modulate = Color.BLACK                        # Plataforma muerte: negra

func _on_body_entered(body: Node2D) -> void:
	if body.is_in_group("jugador"):                              # Si el cuerpo que entra es el jugador
		
		match tipo:

			TipoPlataforma.FRAGIL:
				await get_tree().create_timer(0.5).timeout       # Espera medio segundo
				queue_free()                                      # Destruye la plataforma

			TipoPlataforma.REBOTE:
				if body.has_method("puede_rebotar"):             # Si el jugador tiene el método puede_rebotar
					body.puede_rebotar(fuerza_rebote)             # Llama al método para hacer rebotar con fuerza
				else:
					body.velocity.y = body.brinco * fuerza_rebote # Si no, modifica directamente la velocidad vertical

			TipoPlataforma.MUERTE:
				await get_tree().reload_current_scene()          # Recarga la escena si toca plataforma muerte

	pass  # Esto no hace nada, puedes eliminarlo

func oscilar():
	var tween = create_tween()                                  # Crea un tween para animar suavemente la posición
	tween.tween_property(self, "position:x", position.x + 100, 2) # Mueve 100px a la derecha en 2 segundos
	tween.tween_property(self, "position:x", position.x - 100, 2) # Mueve 100px a la izquierda en 2 segundos
	tween.set_loops()                                           # Hace que la animación se repita indefinidamente

```
**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**

### 🦋checkpoint.gd
**-** Este script pertenece a un nodo Area2D que actúa como un punto de de guardado automatico en caso de que el jugardor no pueda pasar el nivel.

Los checkpoint definidos son:  
🔴   una bandera que la pasar por ella guarda tu posicion para reaparecer en caso de morir

**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**
```
func _ready():
	# Conecta la señal 'body_entered' de este nodo con la función '_on_body_entered' para que se llame automáticamente cuando un cuerpo entre en el área
	connect("body_entered", Callable(self, "_on_body_entered"))

func _on_body_entered(body):
	# Cuando un cuerpo entra en el área, se verifica si pertenece al grupo 'jugador'
	if body.is_in_group("jugador"):
		body.save_game()  # Llama a la función 'save_game' del jugador para guardar la posición y escena
		body.mostrar_mensaje("Checkpoint guardado")  # Muestra un mensaje que confirma que el checkpoint fue guardado


```
**ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷ˏˋ°•*⁀➷**
●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●～●
<div align="center">
<h2><strong>⭐videos del funcionamiento del juego/proyecto⭐</strong></h2>
</div>

Video 1

https://github.com/user-attachments/assets/58e8acf9-36f2-4867-8f69-8428893d0a39


Video 2

https://github.com/user-attachments/assets/b6a9b3b8-56de-44d9-a6c5-12801fecce6a

<div align="center">
<h2><strong>⭐Comentarios⭐</strong></h2>
</div>

fue muy complicado al inicio por que la falta de timpo ya que recientemente consegui computadora y eso me difuculto mucho poder desarrollar el juego y en los momentos de querer guardar se corrompian el juego y no sabia el por que nunca lo descubri asi que me puse a investigar diferentes metodos.
