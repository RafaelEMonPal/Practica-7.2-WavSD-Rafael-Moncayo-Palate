# Practica-7.2-WavSD-Rafael-Moncayo-Palate

## Codi de la pràctica 

```cpp
#include <Arduino.h>
#include "Audio.h"
#include "SD.h"
#include "FS.h"
// Digital I/O used
#define SD_CS 5
#define SPI_MOSI 23
#define SPI_MISO 19
#define SPI_SCK 18
#define I2S_DOUT 25
#define I2S_BCLK 27
#define I2S_LRC 26

Audio audio;
void setup(){
pinMode(SD_CS, OUTPUT);
digitalWrite(SD_CS, HIGH);
SPI.begin(SPI_SCK, SPI_MISO, SPI_MOSI);
Serial.begin(115200);
SD.begin(SD_CS);
audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
audio.setVolume(10); // 0...21
audio.connecttoFS(SD, "Ensoniq-ZR-76-01-Dope-77.wav");
} // Falta archivo de audio para la salida ERROR

void loop(){
audio.loop();
}
// optional
void audio_info(const char *info){
Serial.print("info"); Serial.println(info);
}
void audio_id3data(const char *info){ //id3 metadata
Serial.print("id3data"); Serial.println(info);
}
void audio_eof_mp3(const char *info){ //end of file
Serial.print("eof_mp3"); Serial.println(info);
}
void audio_showstation(const char *info){
Serial.print("station"); Serial.println(info);
}
void audio_showstreaminfo(const char *info){
Serial.print("streaminfo "); Serial.println(info);
}
void audio_showstreamtitle(const char *info){
Serial.print("streamtitle "); Serial.println(info);
}
void audio_bitrate(const char *info){
Serial.print("bitrate"); Serial.println(info);
}
void audio_commercial(const char *info){ //duration in sec
Serial.print("commercial "); Serial.println(info);
}
void audio_icyurl(const char *info){ //homepage
Serial.print("icyurl"); Serial.println(info);
}
void audio_lasthost(const char *info){ //stream URL played
Serial.print("lasthost"); Serial.println(info);
}
void audio_eof_speech(const char *info){
Serial.print("eof_speech "); Serial.println(info);
}

```
## Explicació de la pràctica

El codi comença declarant els pins per on volem que ens entri el lector de SD, i els pins I2S de l'altaveu. Es declara un objecte audio i el setup el que ens fa és dir-li a la SD que busqui un fitxer anomenat "Ensoniq-ZR-76-01-Dope-77.wav" amb la funció:"**audio.connecttoFS**" i després que la tregui per els pins I2S de sortida.
