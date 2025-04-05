### Vectores de prueba  

#### 1. Pruebas en CONFIGURACIÓN  
- CONFIGURACIÓN,	Botón A (evento 'A'),	Incrementar contador,	CONFIGURACIÓN	[X]
- CONFIGURACIÓN,	Botón B (evento 'B'),	Decrementar contador (mínimo 10),	CONFIGURACIÓN	[X]
- CONFIGURACIÓN,	Botón A cuando contador es 60,	No incrementar,	CONFIGURACIÓN	[X]
- CONFIGURACIÓN,	Botón B cuando contador es 10,	No decrementar,	CONFIGURACIÓN	[X]
- CONFIGURACIÓN,	Gesto "shake",	Cambiar a ARMADO,	ARMADO	[X]

#### 2. Pruebas en ARMADO
- ARMADO,	Tiempo transcurre (1s),	Reducir contador en 1,	ARMADO	[X]
- ARMADO,	Tiempo transcurre hasta llegar a 0,	Activar explosión,	EXPLOSIÓN	[X]
- ARMADO,	Ingreso de secuencia incorrecta,	No cambiar estado,	ARMADO	[X]
- ARMADO,	Ingreso de secuencia correcta (A, B, A, S),	Regresar a CONFIGURACIÓN con contador en 20,	CONFIGURACIÓN	[X]  

### 3. Pruebas con Interacciones no Modeladas  
- CONFIGURACIÓN,	Gesto "shake" (sin pasar por ARMADO),	No cambiar estado,	CONFIGURACIÓN	[X]
- ARMADO,	Presionar botón A o B,	No cambiar estado,	ARMADO	[X]
- SECUENCIA DE DESACTIVADO,	Ingresar secuencia parcial (A, B),	No cambiar estado,	SECUENCIA DE DESACTIVADO	[X]
- EXPLOSIÓN,	Ingresar secuencia de desactivado,	No debe afectar el estado,	EXPLOSIÓN	[X]

