# In The Rain

I was inspired by the classic clip from Singing in the Rain, so I wanted to simulate the effect of rain through open frameworks, where the size of the rain is adjusted through the arduino and an umbrella follows the movement of the mouse in the screen.

![rain](https://git.arts.ac.uk/storage/user/555/files/56c39565-2581-4efd-aa8a-954e073b8862)

The reference for the falling particle effect is math's particlesExample in Example.The effect of particlesExample is shown in the following video.

https://git.arts.ac.uk/storage/user/555/files/202454bb-c71f-4075-850c-da347a0628f6

Created a simulated rain effect

https://git.arts.ac.uk/storage/user/555/files/52adf7d1-eeaa-4979-a225-014fe810cbf8

The size of the rain is controlled by transmitting openframeworks via the Arduino's potentiometer connection.

**Adjusted the length and fall speed of particle effects to represent the changing size of the rain.**

```
{

const int potPin=A0; 
int w=1025;
int potVal;

void setup() {
  Serial.begin(9600); // Open the serial port and set the baud rate of the serial port

}

void loop() {
  if (Serial.available()) { // If there is any data available
    potVal = analogRead(potPin); // Reading analogue values from the A0 pin
    if(potVal!=w){
    Serial.print(Math.floor(potVal/11));  // Sending serial values to the serial monitor
    }
    w=potVal;
    delay(500);                        //delay
  }
}

}
```
he main time was spent on the Arduino to openframeworks data transfer. The data transferred was a value passed as a char type, but the char to int conversion would report an error due to storage space issues, and reducing the number of bits of data char would overflow the content of the passed data, so the mapping of the passed data was turned down in advance in the arduino code. int a = atoi(receivedData) inadvertently found that atoi could be performed. 

I don't know if it's the performance of the computer or the performance of the software in the transfer of data, but running the project in openframeworks linked to Arduino causes the whole file to fizzle out after a certain amount of time and forces the software to close. At the moment there is no solution but to run the project for a short time.

https://git.arts.ac.uk/storage/user/555/files/d705f481-c685-49ab-b7e0-ffed7009e0f3

For a better presentation it is better to use the gui to adjust the size of the rain.

https://git.arts.ac.uk/storage/user/555/files/d8956e3e-b7df-4711-a4f4-50f6ddaad14c

The distance between the position of the vec mouse and the particle is created, and when the distance is less than 100, the velocity is reversed by 0.8 to create the effect of raindrops jumping on the umbrella.

```
{
    // move from the mouse
    glm::vec2 mouseVec = glm::vec2(ofGetMouseX(), ofGetMouseY()) - pos;
    if(glm::length(mouseVec) < 100) {
        mouseVec = glm::normalize(mouseVec);
        vel = -vel*0.5;
    }
}
```

https://git.arts.ac.uk/storage/user/555/files/54e33b56-7ab3-437e-8f94-21c0444903c2

## Final result

https://git.arts.ac.uk/storage/user/555/files/c24ae9e2-e774-4929-9a7c-b25692cff821

There are three categories of treatment for the interaction of umbrellas with rain.
1 No change
2 Jump after encountering umbrella, stay on umbrella, umbrella moves x falls
3 Disappear on encountering umbrella so that the number of raindrops above and below the umbrella is not the same

However, it is not possible to see soberly the bouncing effect of the umbrella when it meets the rain. version2 is showing all the raindrops (particles) as category 2 to amplify the bouncing effect.

## version2
https://git.arts.ac.uk/storage/user/555/files/30fe72f6-4947-4f08-a6d3-4abff75bb9ed



