## Spring to Json to Vue3

#### Spring Starter
- starter-web
- spring-boot-devtools
- added demo `User.java` and `MessageController.java`

``` console
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32
$ unzip 230317thymeleafStarter.zip
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32
$ curl http://localhost:8080/api/messages/hello
Full Stack Java with Spring Boot and VueJS!
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32
$ curl http://localhost:8080/api/messages/json
{"id":1,"name":"User","birthDate":1681875697987,"emails":["user@gmail.com","user@yahoo.com"]}
```

#### npm init vue@latest
``` console
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src
$ npm init vue@latest

Vue.js - The Progressive JavaScript Framework
√ Project name: ... frontend
√ Add TypeScript? ... No
√ Add JSX Support? ... No
√ Add Vue Router for Single Page Application development? ... No
√ Add Pinia for state management? ... No
√ Add Vitest for Unit Testing? ... Yes
√ Add an End-to-End Testing Solution? » No
√ Add ESLint for code quality? ... No
Scaffolding project in C:\Users\AlvinNg\zero1Wk32\flipSpringVue\src\frontend...
Done. Now run:
  cd frontend
  npm install
  npm run dev

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src
$ cd frontend
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ npm install
...
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ npm run dev
...
```
#### npm run test:unit
``` console
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ npm run test:unit
...
```
### config Spring url to Vue

#### vite.config.js
``` js
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        ws: true,
        changeOrigin: true
      }
    },
    cors: false
  }
})
```
#### ./components/DisplayJson.vue
``` vue
<script setup>
import { ref, watchEffect } from 'vue'

const API_URL = `/api/messages/json`
const idText = ref([])

function getJson() {
  console.log(">>>>>")
  watchEffect(async () => {
    const url = `${API_URL}`
    idText.value = await (await fetch(url)).json()
  })
}
</script>
<template>
  <div>
    <button @click="getJson">get JSON</button>

    <div>
      ID: {{ idText.id }}
    </div>
    <div>
      Name: {{ idText.name }}
    </div>
    <div>
      DOB: {{ idText.birthDate }}
    </div>
    <div>
      Email: {{ idText.emails }}
    </div>
  </div>
</template>
```
#### edit App.vue
``` vue
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import DisplayJson from './components/DisplayJson.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <DisplayJson />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

...
```
---
### Reference
``` console
AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue
$ ls
bin/  HELP.md  mvnw*  mvnw.cmd  pom.xml  src/  target/

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src
$ ls
frontend/  main/  test/

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ ls
index.html     package.json       public/    src/            vitest.config.js
node_modules/  package-lock.json  README.md  vite.config.js

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ ls src/
App.vue  assets/  components/  main.js

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ ls src/components
__tests__/  DisplayJson.vue  HelloWorld.vue  icons/  TheWelcome.vue  WelcomeItem.vue

AzureAD+AlvinNg@LAPTOP-OJGI6SOT MINGW64 ~/zero1Wk32/flipSpringVue/src/frontend
$ ls src/components/__tests__
HelloWorld.spec.js
```
package.json
``` json
{
  "name": "frontend",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "test:unit": "vitest"
  },
  "dependencies": {
    "vue": "^3.2.47"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^4.0.0",
    "@vue/test-utils": "^2.3.0",
    "jsdom": "^21.1.0",
    "vite": "^4.1.4",
    "vitest": "^0.29.1"
  }
}
```
main.js
``` js
import { createApp } from 'vue'
import App from './App.vue'

import './assets/main.css'

createApp(App).mount('#app')
```
HelloWorld.spec.js
``` js
import { describe, it, expect } from 'vitest'

import { mount } from '@vue/test-utils'
import HelloWorld from '../HelloWorld.vue'

describe('HelloWorld', () => {
  it('renders properly', () => {
    const wrapper = mount(HelloWorld, { props: { msg: 'Hello Vitest' } })
    expect(wrapper.text()).toContain('Hello Vitest')
  })
})
```
index.html
``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```
MessageController.java
``` java
package com.zero1.flip;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.fasterxml.jackson.core.JsonProcessingException;

@RestController
@RequestMapping("/api/messages")
public class MessageController {

    /** $ curl http://localhost:8080/api/messages/hello */
    @GetMapping("/hello")
    public String hello() {
        return "Full Stack Java with Spring Boot and VueJS!";
    }

    /**
     * $ curl http://localhost:8080/api/messages/json
     * {"id":1,"name":"User","birthDate":1681176823185,"emails":["user@gmail.com","user@yahoo.com"]}
     */
    @GetMapping("/json")
    public String soutJson() {
        User u = new User();
        String json = "";
        try {
            json = u.soutJson();
        } catch (JsonProcessingException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        System.out.println(json);
        return json;
    }
}
```
User.java
``` java
package com.zero1.flip;

import java.util.Calendar;
import java.util.HashSet;
import java.util.Set;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
public class User {
    private Long id;
    private String name;
    private Calendar birthDate;
    private Set<String> emails;
    public Long getId() {
        return id;
    }
    public void setId(Long id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public Calendar getBirthDate() {
        return birthDate;
    }
    public void setBirthDate(Calendar birthDate) {
        this.birthDate = birthDate;
    }
    public Set<String> getEmails() {
        return emails;
    }
    public void setEmails(Set<String> emails) {
        this.emails = emails;
    }
    public String soutJson() throws JsonProcessingException {
        User user = new User();
        user.setId(1L);
        user.setName("User");
        user.setBirthDate(Calendar.getInstance());
        user.setEmails(new HashSet<String>());
        user.getEmails().add("user@gmail.com");
        user.getEmails().add("user@yahoo.com");

        ObjectMapper mapper = new ObjectMapper();

        String json = mapper.writeValueAsString(user);
        return json;
    }

    public static void main(String[] args) throws Exception {
        User u = new User();
        String json =  u.soutJson();
        System.out.println(json);
    }
    
}
```
pom.xml
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.0.4</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.zero1</groupId>
	<artifactId>flip</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>flip</name>
	<description>Flip page for IdScan</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-thymeleaf</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```
