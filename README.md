#include "mbed.h"
#include"DHT.h" //Header file for the sensor.
DHT sensor(D4, DHT11); 

int main()
{
    int error=0;
    float h=0.0f, c=0.0f, f=0.0f,k=0.0f, dp=0.0f,dpf=0.0f;
    while (1) 
    {
        wait(0.2f);
        error = sensor.readData();
            if(error == 0)
            {
                c = sensor.ReadTemperature(CELCIUS);
                f = sensor.ReadTemperature(FARENHEIT);
                k = sensor.ReadTemperature(KELVIN);
                h = sensor.ReadHumidity();
                dp = sensor.CalcdewPoint(c,h);
                dpf = sensor.CalcdewPointFast(c,h);
                printf("Temperature\n Kelvin: %4.2f \n Farenheit: %4.2f \n Celcius: %4.2f \n", k,f,c);
                printf("Humidity is %4.2f \n Dewpoint: %4.2f \n Dewpoint Fast: %4.2f \n", h, dp, dpf);
            }
            else 
            {
                printf("Error: %d", error);
            }
    }
