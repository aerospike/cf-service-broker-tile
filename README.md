## Aerospike Service Broker Tile for Cloud Foundry

This project creates a Pivotal Cloud Foundry Service Broker tile that can be used to managed application bindings to an existing Aerospike database. The project requires the [Aerospike Service Broker](https://github.com/aerospike/cf-aerospike-service-broker.git) Spring Boot application. It also requires the [Pivotal Tile Generator](https://github.com/cf-platform-eng/tile-generator) project.

### Getting Started

#### Option 1: Install Pre-built Tile
1. Import the ```aerospike-service-broker-X.X.X.pivotal``` tile from the root directory of this project into Cloud Foundry via the Ops Manager

#### Option 2: Build the Tile
1. Clone the [Aerospike Service Broker](https://github.com/aerospike/cf-aerospike-service-broker.git) project and from the root directory of the project run ```gradle assemble```
2. Copy build/library/service-broker-0.0.1-SNAPSHOT.jar from the Aerospike Service Broker project to the ```resources``` directory of this project
3. Clone the [Pivotal Tile Generator](https://github.com/cf-platform-eng/tile-generator) project
4. Add the bin directory from the Pivotal Tile Generator project to the path (macOS: ```export PATH=$PATH:/pathToTileGeneratorProject/bin```)
5. Run ```tile build``` from the root directory of this project
6. This will create an ```aerospike-service-broker-X.X.X.pivotal``` file in the product directory. This is the service broker tile that can be imported into Pivotal Cloud Foundry.

### Configuration

The Service Broker tile has an "Aerospike Configuration" tab that is used to configure the service broker to point to the existing Aerospike DB. On that tab, fill in the hostname and port of the Aerospike cluster and also select the license type (community or enterprise).

The Service Broker tile requires that the Aerospike database have a namespace ```cf_admin``` configured. Registering the broker will fail if the ```cf_admin``` namespace doesn't exist. The broker uses this namespace to store service entities and serice binding entities.

The Service Broker will expose all namesapaces (except the ```cf_admin``` namespace) as plans which can be used for creating services.

### Example Application

See the [Aerospike Cloud Foundry Example Application](https://github.com/aerospike/cf-example-application.git) to see an application that uses the service broker to bind/unbind to an Aerospike database.
