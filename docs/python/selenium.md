# Web Scraping con Selenium

Vamos a scrapear el sitio de Latam para averiguar datos de vuelos en funcion el origen y destino, fecha y cabina. La información que esperamos obtener de cada vuelo es:

- Precio(s) disponibles
- Horas de salida y llegada (duración)
- Información de las escalas

**¡Empecemos!** Utilicemos lo aprendido hasta ahora para lograr el objetivo propuesto

Selenium es una herramienta que nos permitirá controlar un navegador y podremos utilizar las funcionalidades del motor de JavaScript para cargar el contenido que no viene en el HTML de la página. Para esto necesitamos el módulo webdriver.

Para poder utilizar Selenium con Python hay que seguir una serie de pasos que están detallados a continuación.

1. Instalar los bindings de Selenium para Python. Éstos nos permitirán controlar un navegador desde el código.
    Ejecutar:

    `pip install selenium`
    
    O si estás utilizando Anaconda, puedes instalarlo con:

    `conda install -c conda-forge selenium`
    
2. Selenium necesita un driver para poder generar una interfaz con el navegador. Dependiendo el navegador que uses, deberás descargar un driver distinto. Acá te dejo un listado de los links de descarga para los distintos navegadores. Asegurate de descargar el que corresponda con la versión de tu navegador:

    - Chrome: https://sites.google.com/a/chromium.org/chromedriver/downloads
    - Edge: https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/
    - Firefox: https://github.com/mozilla/geckodriver/releases
    - Safari: https://webkit.org/blog/6900/webdriver-support-in-safari-10/
    
3. Es importante que el archivo descargado esté en una carpeta accesible desde la Jupyter Notebook, ya que necesitaremos referenciarlo desde el código para poder utilizarlo.

`pip install webdriver-manager`

```python
import requests
from bs4 import BeautifulSoup

url = "https://www.latam.com/es_co/apps/personas/booking?fecha1_dia=20&fecha1_anomes=2020-03&fecha2_dia=20&fecha2_anomes=2020-03&from_city2=MDE&to_city2=BOG&auAvailability=1&ida_vuelta=ida_vuelta&vuelos_origen=Bogot%C3%A1&from_city1=BOG&vuelos_destino=Medell%C3%ADn&to_city1=MDE&flex=1&vuelos_fecha_salida_ddmmaaaa=05/03/2020&vuelos_fecha_regreso_ddmmaaaa=07/03/2020&cabina=Y&nadults=2&nchildren=0&ninfants=0&cod_promo=&stopover_outbound_days=0&stopover_inbound_days=0&application=#/"

r = requests.get(url)
print(r.status_code)

s = BeautifulSoup(r.text, 'lxml')
print(s.prettify())
```

Output

```
200
<!DOCTYPE html>
<html lang="es">
 <head>
  <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
  <meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible"/>
...
```

Vemos que la respuesta de la página no contiene la información que buscamos, ya que la misma aparece recién después de ejecutar el código JavaScript que está en la respuesta.

## Selenium

```python
import time
from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from selenium.common.exceptions import TimeoutException
```

**Paso 1:** instanciar un driver del navegador

```python
from webdriver_manager.chrome import ChromeDriverManager

options = webdriver.ChromeOptions()
options.add_argument('--incognito')
driver = webdriver.Chrome(ChromeDriverManager().install(), options=options)
```

> Looking for [chromedriver 80.0.3987.106 linux64] driver in cache 
>File found in cache by path [/home/esteban/.wdm/drivers/chromedriver/80.0.3987.106/linux64/chromedriver]

**Paso 2:** hacer que el navegador cargue la página web.

```python
url = "https://www.latam.com/es_co/apps/personas/booking?fecha1_dia=20&fecha1_anomes=2020-03&fecha2_dia=20&fecha2_anomes=2020-03&from_city2=MDE&to_city2=BOG&auAvailability=1&ida_vuelta=ida_vuelta&vuelos_origen=Bogot%C3%A1&from_city1=BOG&vuelos_destino=Medell%C3%ADn&to_city1=MDE&flex=1&vuelos_fecha_salida_ddmmaaaa=05/03/2020&vuelos_fecha_regreso_ddmmaaaa=07/03/2020&cabina=Y&nadults=2&nchildren=0&ninfants=0&cod_promo=&stopover_outbound_days=0&stopover_inbound_days=0&application=#/"

driver.get(url)
```

**Paso 3:** extraer la información de la página

```python
def obtener_precios(vuelo):
    '''
    Función que retorna una lista de diccionarios con las distintas tarifas
    '''
    tarifas = vuelo.find_elements_by_xpath('.//div[@class="fares-table-container"]//tfoot//td[contains(@class, "fare-")]')
    precios = []
    for tarifa in tarifas:
        nombre = tarifa.find_element_by_xpath('.//label').get_attribute('for')
        moneda = tarifa.find_element_by_xpath('.//span[@class="price"]/span[@class="currency-symbol"]').text
        valor = tarifa.find_element_by_xpath('.//span[@class="price"]/span[@class="value"]').text 
        dict_tarifa={nombre:{'moneda':moneda, 'valor':valor}}
        precios.append(dict_tarifa)
        
    return precios

def obtener_datos_escalas(vuelo):
    '''
    Función que retorna una lista de diccionarios con la información de 
    las escalas de cada vuelo
    '''
    segmentos = vuelo.find_elements_by_xpath('//div[contains(@class, "modal-body")]/div/div')
    info_escalas = []
    for segmento in segmentos:
        # Origen
        #origen = segmento.find_element_by_xpath('.//div[@class="departure"]/span[@class="ground-point-name"]').text
        # Hora de salida
        #dep_time = segmento.find_element_by_xpath('.//div[@class="departure"]/time').get_attribute('datetime')
        # Destino
        #destino = segmento.find_element_by_xpath('.//div[@class="arrival"]/span[@class="ground-point-name"]').text
        # Hora de llegada
        #arr_time = segmento.find_element_by_xpath('.//div[@class="arrival"]/time').get_attribute('datetime')
        # Duración del vuelo
        #duracion_vuelo = segmento.find_element_by_xpath('.//span[@class="duration flight-schedule-duration"]/time').get_attribute('datetime')
        # Numero del vuelo
        #numero_vuelo = segmento.find_element_by_xpath('.//span[@class="equipment-airline-number"]').text
        # Modelo de avion
        #modelo_avion =segmento.find_element_by_xpath('.//span[@class="equipment-airline-material"]').text
        if segmento != segmentos[-1]:
            # Duracion de la escala
            #duracion_escala = segmento.find_element_by_xpath('.//div[@class="stop connection"]//p[@class="stop-wait-time"]//time').get_attribute('datetime')
            pass
        else:
            duracion_escala = ''
        
        data_dict={
            #'origen':origen,
            #'dep_time':dep_time,
            #'destino':destino,
            #'arr_time':arr_time,
            #'duracion_vuelo':duracion_vuelo,
            #'numero_vuelo':numero_vuelo,
            #'modelo_avion':modelo_avion,
            #'duracion_escala':duracion_escala,
        }
        info_escalas.append(data_dict)
        
    return info_escalas

def obtener_tiempos(vuelo):
    '''
    Función que retorna un diccionario con los horarios de salida y llegada de cada
    vuelo, incluyendo la duración. 
    Nota: la duración del vuelo no es la hora de llegada - la hora de salida porque
    puede haber diferencia de horarios entre el origen y el destino.
    '''
    # Hora de salida
    salida = vuelo.find_element_by_xpath('.//div[@class="departure"]/time').get_attribute('datetime')
    # Hora de llegada
    llegada = vuelo.find_element_by_xpath('.//div[@class="arrival"]/time').get_attribute('datetime')
    # Duracion
    duracion = vuelo.find_element_by_xpath('.//span[@class="duration"]/time').get_attribute('datetime')
    tiempos = {'hora_salida': salida, 'hora_llegada': llegada, 'duracion': duracion}
    return tiempos

def obtener_info(driver):
    vuelos = driver.find_elements_by_xpath('//li[@class="flight"]')
    print(f'Se encontraron {len(vuelos)} vuelos.')
    print('Iniciando scraping...')
    info = []
    for vuelo in vuelos:
        #obtenemos los tiempos generales de cada vuelo
        tiempos = obtener_tiempos(vuelo)
        
        # Clickeamos sobre el boton de las escalas
        vuelo.find_element_by_xpath('.//div[@class="flight-summary-stops-description"]/button').click()
        escalas = obtener_datos_escalas(vuelo)
        
        # Cerramos el modal
        close_button = driver.find_element_by_xpath('//div[contains(@class, "modal-dialog")]//button[@class="close"]')
        if close_button:
            close_button.click()
        
        # Clickeamos el vuelo para ver los precios
        vuelo.click()
        
        precios = obtener_precios(vuelo)
        
        vuelo.click()
        info.append({'precios':precios, 'tiempos': tiempos, 'escalas':escalas})
        
    return info

delay = 10

try:
    # introducir demora inteligente
    vuelo = WebDriverWait(driver, delay).until(EC.presence_of_element_located((By.XPATH, '//li[@class="flight"]')))
    
    print('La página terminó de cargar')
    
    info_vuelos = obtener_info(driver)
except TimeoutException:
    print('La página tardó demasiado en cargar')
    info_vuelos = []
    
time.sleep(5)
```

Output

```
Se encontraron 17 vuelos.
Iniciando scraping...

[{'precios': [{'LIGHT': {'moneda': '$', 'valor': '252.375'}},
   {'PLUS': {'moneda': '$', 'valor': '294.025'}},
   {'TOP': {'moneda': '$', 'valor': '354.040'}}],
  'tiempos': {'hora_salida': '13:04',
   'hora_llegada': '14:02',
   'duracion': 'PT58M'},
  'escalas': [{}]},
 {'precios': [{'LIGHT': {'moneda': '$', 'valor': '304.264'}},
   {'PLUS': {'moneda': '$', 'valor': '345.914'}},
   {'TOP': {'moneda': '$', 'valor': '405.922'}}],
  'tiempos': {'hora_salida': '14:16',
   'hora_llegada': '15:14',
   'duracion': 'PT58M'},
  'escalas': [{}]},
...
```

**Paso 4:** cerrar el navegador

driver.close()