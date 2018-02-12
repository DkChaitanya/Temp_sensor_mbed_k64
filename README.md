//Reads the Data from DHT11 Temperature/Humidity Sensor which is connected to the NXP Microcontroller FRDM K64 and displays the data on a Serial Terminal (TeraTerm/Putty). The K64 board is connected to the PC through the USB which acts as a UART communication. The DHT Sensor is connected to the K64 board through a Grove Shield. The IDE used here was mbed online compiler.//

#include "mbed.h"
#include"DHT.h"
DHT sensor(D4, DHT11); //sensor is a variable of class DHT. 
/*D4 is the Pin on the Grove Shield to which sensor is connected and 
  DHT11 is the version of the sensor we are using */

int main()
{
    int error=0; 
    float h=0.0f, c=0.0f, f=0.0f,k=0.0f, dp=0.0f,dpf=0.0f; //variables to store the sensor values
    while (1) 
    {
        wait(0.2f); //Data is displayed after certain intervals
        error = sensor.readData(); //readData() is a function which reads the sensor values upon execution
            if(error == 0)
            {
                c = sensor.ReadTemperature(CELCIUS); //ReadTemperature() gets the temperature value from the sensor
                f = sensor.ReadTemperature(FARENHEIT); 
                k = sensor.ReadTemperature(KELVIN);
                h = sensor.ReadHumidity(); //ReadHumidity() reads the humidity sensor value from the sensor
                dp = sensor.CalcdewPoint(c,h); //CalcdewPoint() reads the dew point measurements.
                dpf = sensor.CalcdewPointFast(c,h);
                printf("Temperature\n Kelvin: %4.2f \n Farenheit: %4.2f \n Celcius: %4.2f \n", k,f,c); //Prints the Temperature values
                printf("Humidity is %4.2f \n Dewpoint: %4.2f \n Dewpoint Fast: %4.2f \n", h, dp, dpf); //Prints the Humidity values
            }
            else 
            {
                printf("Error: %d", error); 
            }
    }
}
