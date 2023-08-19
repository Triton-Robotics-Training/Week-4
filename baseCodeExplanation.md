```cpp
#include "main.h"

DigitalOut led(L26);
DigitalOut led2(L27);
DigitalOut led3(L25);

I2C i2c(I2C_SDA, I2C_SCL);

int main(){

    //assigning can handler objects to motor class.
    DJIMotor::s_setCANHandlers(&canHandler1,&canHandler2, false, false); 

    //DEFINE MOTORS, ETC

    //getting initial feedback.
    DJIMotor::s_getFeedback();

    unsigned long loopTimer_u = us_ticker_read();
    unsigned long timeEnd_u;
    unsigned long timeStart_u;

    //DEFINE PIDs AND OTHER CONSTANTS

    while(true){ //main loop
        timeStart_u = us_ticker_read();

        //inner loop runs every 25ms
        if((timeStart_u - loopTimer_u) / 1000 > 25) { 
            loopTimer_u = timeStart_u;
            led = !led; //led blink tells us how fast the inner loop is running

            if (refLoop >= 5) { //ref code runs 5 of every inner loop, 
                refLoop = 0;
                refereeThread(&referee);
            }

            remoteRead(); //reading data from remote

            //MAIN CODE

            timeEnd_u = us_ticker_read();

            DJIMotor::s_sendValues();
        }
        DJIMotor::s_getFeedback();
        ThisThread::s_sleep_for(1ms);
    }
}
```
