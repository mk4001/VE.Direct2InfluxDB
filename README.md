# VE.Direct2InfluxDB
Victron Energy VE.Direct UART data output to InfluxDB.2 using Espressif ESP32

The idea of untying the Smart Solar MPPT 75/15 by Victron Energy from the BLE APP of the smartphone and being able to bring the data to the cloud on InfluxDB (even on Premise is fine anyway) led me to create this project.

The VE.Direct interface on most Victron Energy products is in fact a UART which transmits at a rate of one record per second at 19200 baud.

It is necessary to make a simple adapter cable with the help of a JST 2.0 PH 4 connector easily available both on Amazon and on Aliexpress.

Of the pins of the UART port in question, I only used PINs 1 (GND) and 3 (TX), then subsequently connected to Serial2 of a Wroom 32 ESP module (Ports GND and GPIO16).

<img width="1369" alt="Screenshot 2023-07-20 at 09 47 55" src="https://github.com/mk4001/VE.Direct2InfluxDB/assets/50479511/780e0403-754e-42f9-90fa-479fb00701fc">

data, as I said, flow from the UART port at the rate of one record per second.

Detailed documentation of the fields, their format and content is gathered here:

https://www.victronenergy.com/upload/documents/VE.Direct-Protocol-3.33.pdf

Once the record has been captured on the ESP32, it is necessary to parse the fields and collect the data of what we need before sending them to InfluxDB.2

It's easy to create a free account on InfluxDB in the cloud, while for the more daring, you can download the entire suite needed for on-premise installation for a Raspberry PI for free.

You can start directly in the Cloud from here:

https://cloud2.influxdata.com/signup

Once logged into InfluxDB, you have to create a new Bucket (in short, a DB) and related Token which you then have to copy into the code attached here together with the ID of your organization. Easy.

When your Bucket is finally full of data you can decide to create a Dashbouard on Grafana (always in the cloud, always free)

https://grafana.com/auth/sign-up/create-user?pg=hp&plcmt=hero-btn1&cta=create-free-account

With a little imagination and above all practice, you can even create dashboards like these:

![image1](https://github.com/mk4001/VE.Direct2InfluxDB/assets/50479511/0b3f3881-2aa3-4213-99fa-47e8b954535b)

![image2](https://github.com/mk4001/VE.Direct2InfluxDB/assets/50479511/179841d6-7990-4e45-8d7f-5db96ba6c5a7)

