# PMf, Agrosmart

If technology is the challenge, we are the ones that take it and make it

Introducing you the new way of connectivity in the farms of the future,

We´ve designed a case for the XDK system that allows the sensors to work in any kind of environment, the first step into this platform would be the placement of the product over the crop field every 70m in order to get a grid over it.

All the devices would connect to a Sigfox network, every device have the ability to measure the humidity, temperature and atmospheric pressure, with this information, the device would be able to water the surrounding area, call for action and keep the user informed every minute about the status of the field

through the data collected by the changes in temperature and humidity, the system will be able to warn the user about the beginning of plagues or any kind of pests,

The next step into this system would be the use of drones to fertilize the crop fields in the most optimal way, using only the necessary fertilizer over the affected areas, in just one step you can request the service

Our system will reduce the waste or excess of water and fertilizer, saving time and money for every kind of market, from the little farmer to the big production companies



package main;
import platforms.xdk110;

/*Configuracion */
setup light{
	manual_mode = true;
	integration_time = MS_800;
	high_brightness = false;
	
}

setup environment{
	power_mode = Normal;
	temperature_oversampling = OVERSAMPLE_8X;
	humidity_oversampling = OVERSAMPLE_8X;
}

setup accelerometer{
	range = Range_16G;
	bandwidth = BW_7_81Hz;
	any_motion_threshold = 10;
}	

setup red: WLAN{
	ssid = "Computadora_magica";
	authentication = Personal(psk = "computadora123");
	ipConfiguration = Dhcp();
}

setup broker: MQTT{
	transport = red;
	url = "mqtt://broker.mqttdashboard.com";
	clientId = "PMf";
	keepAliveInterval = 60;
	cleanSession = false;
	
	var topic_light = topic("xdk_workshop/IRA_031196/light",0);
	var topic_temp = topic("xdk_workshop/IRA_031196/temp",0);
	var topic_motion = topic("xdk_workshop/IRA_031196/motion",0);
	var topic_hum = topic("xdk_workshop/IRA_031196/hum",0);
}


/*Acciones */
every 3 seconds{
	var luz = light.intensity.read();
	print(`Intensidad de la luz: ${luz} milliLuxes\n`);
	broker.topic_light.write(`Intensidad de la luz: ${luz} milliLuxes\n`);

package main;
import platforms.xdk110;

/*Configuracion */
setup light{
	manual_mode = true;
	integration_time = MS_800;
	high_brightness = false;
	
}

setup environment{
	power_mode = Normal;
	temperature_oversampling = OVERSAMPLE_8X;
	humidity_oversampling = OVERSAMPLE_8X;
}

setup accelerometer{
	range = Range_16G;
	bandwidth = BW_7_81Hz;
	any_motion_threshold = 10;
}	

setup red: WLAN{
	ssid = "Computadora_magica";
	authentication = Personal(psk = "computadora123");
	ipConfiguration = Dhcp();
}

setup broker: MQTT{
	transport = red;
	url = "mqtt://broker.mqttdashboard.com";
	clientId = "PMf";
	keepAliveInterval = 60;
	cleanSession = false;
	
	var topic_light = topic("xdk_workshop/IRA_031196/light",0);
	var topic_temp = topic("xdk_workshop/IRA_031196/temp",0);
	var topic_motion = topic("xdk_workshop/IRA_031196/motion",0);
	var topic_hum = topic("xdk_workshop/IRA_031196/hum",0);
}


/*Acciones */
every 3 seconds{
	var luz = light.intensity.read();
	print(`Intensidad de la luz: ${luz} milliLuxes\n`);
	broker.topic_light.write(`Intensidad de la luz: ${luz} milliLuxes\n`);	
}

every 4000 milliseconds{
	var valorTemperatura = environment.temperature.read();
	print(`Temperatura: ${valorTemperatura} milliCelsius\n`);
	broker.topic_temp.write(`Temperatura: ${valorTemperatura} milliCelsius\n`);
}

every 5 second{
	var humedad = environment.humidity.read();
	print(`Humedad: ${humedad} porcentaje\n`);
	broker.topic_hum.write(`Humedad: ${humedad} porcentaje\n`);
}
	
}

every 4000 milliseconds{
	var valorTemperatura = environment.temperature.read();
	print(`Temperatura: ${valorTemperatura} milliCelsius\n`);
	broker.topic_temp.write(`Temperatura: ${valorTemperatura} milliCelsius\n`);
}

every 5 second{
	var humedad = environment.humidity.read();
	print(`Humedad: ${humedad} porcentaje\n`);
	broker.topic_hum.write(`Humedad: ${humedad} porcentaje\n`);
}
