```cpp
#include "main.h"

DigitalOut led(L26);
DigitalOut led2(L27);
DigitalOut led3(L25);

I2C i2c(I2C_SDA, I2C_SCL);

int main(){

    DJIMotor::setCANHandlers(&canHandler1,&canHandler2, false, false);

    DJIMotor::getFeedback();

    //DEFINE MOTORS, ETC

    unsigned long loopTimer = us_ticker_read();
    unsigned long timeEnd;
    unsigned long timeStart;

    //DEFINE PIDs AND OTHER CONSTANTS

    while(true){
        timeStart = us_ticker_read();

        if((timeStart - loopTimer) / 1000 > 25) {
            loopTimer = timeStart;
            led = !led;

            if (refLoop >= 5) {
                refLoop = 0;
                refereeThread(&referee);
            }

            remoteRead();

            //MAIN CODE

            timeEnd = us_ticker_read();

            DJIMotor::sendValues();
        }
        DJIMotor::getFeedback();
        ThisThread::sleep_for(1ms);
    }
}
```
