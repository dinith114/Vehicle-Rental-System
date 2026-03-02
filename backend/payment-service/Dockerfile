# Payment Service Dockerfile
# Orchid Vehicle Rental System
# 
# Build: docker build -t payment-service .
# Run: docker run -p 8084:8084 payment-service

FROM eclipse-temurin:21-jre-alpine

# Security: Run as non-root user
RUN addgroup -S spring && adduser -S spring -G spring

WORKDIR /app

# Copy the pre-built JAR file
COPY target/payment-service-*.jar app.jar

# Change ownership to non-root user
RUN chown -R spring:spring /app

# Switch to non-root user (Security best practice)
USER spring:spring

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=30s --retries=3 \
  CMD wget --quiet --tries=1 --spider http://localhost:8084/actuator/health || exit 1

EXPOSE 8084

# JVM tuning for containers
ENTRYPOINT ["java", \
  "-XX:+UseContainerSupport", \
  "-XX:MaxRAMPercentage=75.0", \
  "-Djava.security.egd=file:/dev/./urandom", \
  "-jar", "app.jar"]
