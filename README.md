JIALIN ZHAO
s3633197

# the circle doesn't work so i did it in my own one also the github, https://github.com/s3633197/assignment-1-student-s3633197 it is public. 
# i will put the screenshots of circleci test and github merge in this file

![image](https://user-images.githubusercontent.com/53294143/114294501-b6c2e380-9ad1-11eb-9738-16156e7a2ecf.png)

# ● Analysis of the problem (What are you actually trying to solve) ( 5%)
    - unit-test:
        Ensure that the logic behind each individual component of the code works as we expect
    - lint-test:
        Avoid low-level errors and unify code style
    - integration-test:
        Ensure that the function of one or more components when working together is what we expect
    - code-coverage:
        Want to use code coverage to indicate the quality of the code
        a good test usually has 80 to 90 percentage code coverage.
    - failure-condition:
        Check if there is a security problem, if yes, exit with a exit code
        exit code 0 means no security issues
        others means something wrong
    - package/artefact:
        a tar file contain all automated tests is needed
        used to run in different environments 

# ● Explain and Justify the solution (How does the solution work) (10%)
    - unit-test:
        - checkout
        - install-deps
            checkout and call install-deps in commmands to insall dependency
        cd src
        npm run test-unit
            change to src folder and call the test-unit script in package.json
    - lint-test:
        using ESLint tool, call test-lint in package.json
    - integration-test:
        - image: circleci/node:lts
        - image: mongo:4.0
            multiple docker containers run at once to support integration testing with dependant services
        npm run test-integration
            run the test-integration script in package.json
    - code-coverage
        add --coverage into package.json to show the code coverage. add a new script or just add it into unit test
        then call it using npm run
    - failure-condition:
        find out the sec parameter(jq .total_count.sec) from sast-output.json(cat sast-ouput.json) through(|) and print it
        exit with a exit code(code exit)
    - package/artefact:
        npm pack
            produce a tar file name simpletodoapp-1.0.0.tgz(<name>-<version>.tgz)
        - store_artifacts
            upload to artefact store
        - package:
          filters:
            branches:
              only:
                - master
            only run in master branch


![image](https://user-images.githubusercontent.com/53294143/114294546-14efc680-9ad2-11eb-8f93-f92bb4ece5f0.png)
![image](https://user-images.githubusercontent.com/53294143/114294552-1caf6b00-9ad2-11eb-9947-480007668f8d.png)
![image](https://user-images.githubusercontent.com/53294143/114294557-246f0f80-9ad2-11eb-91e1-5c41cf4fb622.png)
![image](https://user-images.githubusercontent.com/53294143/114294585-51232700-9ad2-11eb-8652-dc8cf30840f0.png)
![image](https://user-images.githubusercontent.com/53294143/114294587-554f4480-9ad2-11eb-9fde-11fcdc4cd40b.png)
![image](https://user-images.githubusercontent.com/53294143/114294589-58e2cb80-9ad2-11eb-95de-f7a0d190f136.png)
![image](https://user-images.githubusercontent.com/53294143/114294593-5d0ee900-9ad2-11eb-822d-50ac6b2b0dd0.png)
![image](https://user-images.githubusercontent.com/53294143/114294596-613b0680-9ad2-11eb-963d-4ff8c8db3ac6.png)
![image](https://user-images.githubusercontent.com/53294143/114294605-6dbf5f00-9ad2-11eb-981a-58f02a6a99a3.png)
![image](https://user-images.githubusercontent.com/53294143/114294608-71eb7c80-9ad2-11eb-87e0-1d0d5bf844b2.png)
![image](https://user-images.githubusercontent.com/53294143/114294611-76b03080-9ad2-11eb-8d41-23e404d55c78.png)
![image](https://user-images.githubusercontent.com/53294143/114294615-79ab2100-9ad2-11eb-9085-bb24ccf49b3a.png)
![image](https://user-images.githubusercontent.com/53294143/114294618-7c0d7b00-9ad2-11eb-84b3-75ecf3677a71.png)
![image](https://user-images.githubusercontent.com/53294143/114294624-80399880-9ad2-11eb-80c8-f42741f141d2.png)
![image](https://user-images.githubusercontent.com/53294143/114294642-98111c80-9ad2-11eb-9a93-05f1e4c79abe.png)
![image](https://user-images.githubusercontent.com/53294143/114294646-9cd5d080-9ad2-11eb-9e13-085232516045.png)
![image](https://user-images.githubusercontent.com/53294143/114294648-9f382a80-9ad2-11eb-9fcf-74b0693d7d2e.png)



# Simple Todo App with MongoDB, Express.js and Node.js
The ToDo app uses the following technologies and javascript libraries:
* MongoDB
* Express.js
* Node.js
* express-handlebars
* method-override
* connect-flash
* express-session
* mongoose
* bcryptjs
* passport
* docker & docker-compose

## What are the features?
You can register with your email address, and you can create ToDo items. You can list ToDos, edit and delete them. 

# How to use
First install the depdencies by running the following from the root directory:

```
npm install --prefix src/
```

To run this application locally you need to have an insatnce of MongoDB running. A docker-compose file has been provided in the root director that will run an insatnce of MongoDB in docker. TO start the MongoDB from the root direction run the following command:

```
docker-compose up -d
```

Then to start the application issue the following command from the root directory:
```
npm run start --prefix src/
```

The application can then be accessed through the browser of your choise on the following:

```
localhost:5000
```

## Testing

Basic testing has been included as part of this application. This includes unit testing (Models Only), Integration Testing & E2E Testing.

### Linting:
Basic Linting is performed across the code base. To run linting, execute the following commands from the root directory:

```
npm run test-lint --prefix src/
```

### Unit Testing
Unit Tetsing is performed on the models for each object stored in MongoDB, they will vdaliate the model and ensure that required data is entered. To execute unit testing execute the following commands from the root directory:

```
npm run test-unit --prefix src/
```

### Integration Testing
Integration testing is included to ensure the applicaiton can talk to the MongoDB Backend and create a user, redirect to the correct page, login as a user and register a new task. 

Note: MongoDB needs to be running locally for testing to work (This can be done by spinning up the mongodb docker container).

To perform integration testing execute the following commands from the root directory:

```
npm run test-integration --prefix src/
```

### E2E Tests
E2E Tests are included to ensure that the website operates as it should from the users perspective. E2E Tests are executed in docker containers. To run E2E Tests execute the following commands:

```
chmod +x scripts/e2e-ci.sh
./scripts/e2e-ci.sh
```


###### This project is licensed under the MIT Open Source License
