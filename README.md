# ✈️ Pronóstico Turístico - Puno

Aplicación web para predecir las condiciones climáticas en Puno, Perú, diseñada especialmente para planificar viajes turísticos. Utiliza Machine Learning para ofrecer predicciones precisas del estado del clima.

![Python](https://img.shields.io/badge/Python-3.12.10-blue.svg)
![Flask](https://img.shields.io/badge/Flask-3.0.0-green.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.6.1-orange.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 🌟 Características

- 📅 **Selección de fechas intuitiva** estilo aeropuerto
- 🔮 **Predicciones día por día** del estado del clima
- 📊 **Estadísticas del viaje** (días buenos, regulares y malos)
- 📱 **Diseño responsive** adaptable a móviles y tablets
- ⚡ **Interfaz moderna** con animaciones suaves
- 🎨 **Código de colores** para fácil interpretación

## 🎯 Estados del Clima

| Estado | Icono | Color | Descripción |
|--------|-------|-------|-------------|
| **Bueno** | ☀️ | Verde | Excelente para turismo |
| **Regular** | ⛅ | Naranja | Condiciones aceptables |
| **Malo** | 🌧️ | Rojo | No recomendado para actividades al aire libre |

## 📋 Requisitos Previos

- Python 3.12.10 (recomendado)
- pip (gestor de paquetes de Python)
- Archivos de modelo entrenado:
  - `modelo_estado_fecha.pkl`
  - `label_encoder_estado.pkl`

## 🚀 Instalación

### 1. Clonar o descargar el proyecto

```bash
mkdir clima_puno_app
cd clima_puno_app
```

### 2. Crear entorno virtual

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno virtual
# En Windows:
venv\Scripts\activate

# En Linux/Mac:
source venv/bin/activate
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

O instalar manualmente:

```bash
pip install Flask==3.0.0 joblib==1.4.2 pandas==2.2.0 scikit-learn==1.6.1 numpy==1.26.4
```

### 4. Configurar archivos del modelo

Coloca tus archivos `.pkl` en la raíz del proyecto:

```
clima_puno_app/
├── modelo_estado_fecha.pkl      ← Aquí
├── label_encoder_estado.pkl     ← Aquí
├── app.py
├── templates/
│   └── index.html
└── requirements.txt
```

## 🎮 Uso

### Iniciar la aplicación

```bash
python app.py
```

La aplicación estará disponible en:
- Local: http://127.0.0.1:5000
- Red local: http://[tu-ip]:5000

### Usar la aplicación

1. **Selecciona la fecha de llegada** (inicio de tu viaje)
2. **Selecciona la fecha de salida** (fin de tu viaje)
3. Haz clic en **"🔮 Consultar Clima"**
4. Revisa las **estadísticas** y el **pronóstico detallado**

## 📁 Estructura del Proyecto

```
clima_puno_app/
│
├── app.py                       # Aplicación Flask principal
├── templates/
│   └── index.html              # Frontend de la aplicación
├── modelo_estado_fecha.pkl     # Modelo ML entrenado
├── label_encoder_estado.pkl    # Codificador de etiquetas
├── requirements.txt            # Dependencias del proyecto
├── README.md                   # Este archivo
└── venv/                       # Entorno virtual (no incluir en git)
```

## 🛠️ Tecnologías Utilizadas

### Backend
- **Flask 3.0.0**: Framework web
- **scikit-learn 1.6.1**: Machine Learning
- **pandas 2.2.0**: Manipulación de datos
- **joblib 1.4.2**: Serialización de modelos
- **numpy 1.26.4**: Operaciones numéricas

### Frontend
- **HTML5/CSS3**: Estructura y estilos
- **JavaScript (Vanilla)**: Interactividad
- **Fetch API**: Comunicación con el backend

## 🔧 Configuración Avanzada

### Cambiar puerto

Edita `app.py` línea final:

```python
app.run(debug=True, host='0.0.0.0', port=8080)  # Cambiar 5000 por 8080
```

### Modo producción

Para producción, usa un servidor WSGI como Gunicorn:

```bash
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

### Límite de días

Por defecto, la app limita las consultas a 30 días. Para cambiarlo, edita `app.py`:

```python
if dias_diferencia > 30:  # Cambiar 30 por el límite deseado
```

## ⚠️ Solución de Problemas

### Error: "Can't get attribute '_RemainderColsList'"

**Causa**: Incompatibilidad de versión de scikit-learn

**Solución**:
```bash
pip uninstall scikit-learn -y
pip install scikit-learn==1.6.1
```

### Error: "Modelo no encontrado"

**Causa**: Archivos `.pkl` no están en la ubicación correcta

**Solución**: Verifica que `modelo_estado_fecha.pkl` y `label_encoder_estado.pkl` estén en la raíz del proyecto

### Error: "Module not found"

**Causa**: Dependencias no instaladas

**Solución**:
```bash
pip install -r requirements.txt
```

## 📊 Ejemplo de Predicción

### Request (JSON)
```json
{
  "fecha_inicio": "2025-10-21",
  "fecha_fin": "2025-10-25"
}
```

### Response (JSON)
```json
{
  "predicciones": [
    {
      "fecha": "2025-10-21",
      "estado": "Bueno",
      "color": "#10b981",
      "icono": "☀️",
      "descripcion": "Excelente para turismo"
    }
  ],
  "estadisticas": {
    "total": 5,
    "buenos": 3,
    "regulares": 1,
    "malos": 1,
    "porcentaje_bueno": 60.0
  }
}
```

## 🤝 Contribuir

Las contribuciones son bienvenidas. Para contribuir:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/NuevaCaracteristica`)
3. Commit tus cambios (`git commit -m 'Agregar nueva característica'`)
4. Push a la rama (`git push origin feature/NuevaCaracteristica`)
5. Abre un Pull Request

## 📝 Modelo de Machine Learning

El modelo utiliza las siguientes características para predecir:
- `year`: Año
- `month`: Mes
- `day`: Día del mes
- `dayofyear`: Día del año (1-365)
- `weekofyear`: Semana del año
- `season`: Estación del año (Verano, Otoño, Invierno, Primavera)

## 🌡️ Estaciones en Puno

- **Verano**: Diciembre, Enero, Febrero
- **Otoño**: Marzo, Abril, Mayo
- **Invierno**: Junio, Julio, Agosto
- **Primavera**: Septiembre, Octubre, Noviembre

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

## 👥 Autores

- **Tu Nombre** - *Trabajo Inicial* - [Tu GitHub](https://github.com/tu-usuario)

## 🙏 Agradecimientos

- Universidad Nacional del Altiplano - Puno
- Curso de Aprendizaje de Máquina 2025-02
- Datos climáticos de Puno

## 📞 Contacto

Para preguntas o sugerencias, por favor abre un issue en el repositorio.

---

⭐ Si este proyecto te fue útil, considera darle una estrella en GitHub!

**Hecho con ❤️ para turistas de Puno**
