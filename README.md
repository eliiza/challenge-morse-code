# Eliiza Morse Code Challenge

## Intro

In this challenge you're given data containing some old news headlines encoded in *international* [Morse Code](https://morsecode.world/).

## Challenge

Because the data is streaming through a Kafka topic, the challenge consists in tapping onto that topic, decoding the headline and extracting from the **first 1000 records** the headlines that contain the word `australia`.  We are only interested in the headlines with **australia**, **NOT** ~~australian~~ or ~~australians~~.  Save your extraction into an output text file with one headline per line, decoded back to English.

Some relevant info here:
- In morse code there is no distinction between lower/upper case.
- Kafka records in the topic are in plain text format:
  - keys are sequencial, starting in 1;
  - values are encoded in Morse Code.
- The Morse Code is written in traditional notation:
  - dots and dashes with characters separated by a blank and words separated by a slash,
  - *e.g.* a news headline like `Kafka is great` would be `-.- .- ..-. -.- .-/.. .../--. .-. . .- -`.
  
## How to solve the challenge

For this challenge you can use any language you like.  You will most probably use a Scala, Python, Java or JavaScript (Node.js) Kafka client; we have no preference at all.  We provide a `docker-compose.yml` file containing:
- images with a Kafka environment (ZooKeeper and 1 Kafka broker) like this:
  - bootstrap server: `localhost:9092`
  - security protocol: `PLAINTEXT`
  - topic name: `au.com.eliiza.newsheadlines.txt`
- our service that encodes news headlines in international Morse Code, and
- an API that is capable of translating **one** (1) encoded character at a time, *e.g.*:
  - GET http://localhost:8083/kafka-coding-challenge/translate?morse-code=-.- should respond `k`.

## Starting Kafka with docker-compose

First of all, install [Docker Compose](https://docs.docker.com/compose/install/) for your system, if you don't already have it.  Then:

    $ git clone https://github.com/eliiza/challenge-morse-code.git myrepo
    $ cd myrepo
    $ docker-compose up
    
After all the images are downloaded and Kafka is up and running, you should start seeing our service logging the production of news headlines records and serving the translation of morse code characters.  Once you solve the challenge, send us back your code and your output file.

Good luck!!!
