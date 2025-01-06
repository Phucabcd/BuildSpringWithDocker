# Spring Boot Application in Docker

This guide demonstrates how to package a Spring Boot application as a JAR file and run it inside a Docker container.

## Prerequisites

Before proceeding, ensure you have the following tools installed:

- **Java** (JDK 8 or later)
- **Maven**
- **Docker**

## Steps to Package and Run on Docker

### Build Your Docker

Pull Image OpenJDK: You pull the OpenJDK image from Docker Hub

```bash
docker pull openjdk:version
```
Create Container from OpenJDK Image: Once you have the OpenJDK image, you create a container running OpenJDK:

```bash
docker run -it --name openjdk-container openjdk:version
```

### Step 1: Build Your Spring Boot Application

Use Maven to package your Spring Boot application into a JAR file.

```bash
mvn clean package
```

This command will generate a JAR file in the target directory, which you can run locally with:

```bash
java -jar target/name.jar
```

Step 2: Copy the JAR File to Docker Container
Now, copy the generated JAR file into the Docker container. Replace name with your container name, and ensure that the target folder contains the .jar file.

```bash
docker cp target/name.jar name_Container:/tmp
```

Step 3: Verify the JAR File in the Docker Container
To confirm that the JAR file has been successfully copied into the container, execute the following:

```bash
docker exec name ls /tmp
```
You should see name.jar listed in the /tmp directory.

Step 4: Commit the Changes to Docker Image
Commit the changes to create a new Docker image with the Spring Boot application. The CMD instruction defines how the container will run the application.

```
docker commit --change='CMD ["java", "-jar", "/tmp/name.jar"]' name_Container new_name_images:tagName
```
This command will update the image by setting the CMD to run your Spring Boot application when the container starts.

Step 5: Run the Docker Container
Finally, run the newly created Docker image:

```bash
docker run -d --name myapp new_name_images:tagName
```

Conclusion
By following these steps, you can easily package and run your Spring Boot application inside a Docker container. This approach helps streamline deployment, ensuring that your application can run consistently across different environments.

### Tóm tắt:

- Đoạn mã trên là một README.md hoàn chỉnh hướng dẫn các bước đóng gói ứng dụng Spring Boot vào Docker, bao gồm từ xây dựng JAR, sao chép vào container, commit Docker image, và chạy ứng dụng.
- Dockerfile được cung cấp như một tùy chọn để tự động hóa việc tạo image Docker.

