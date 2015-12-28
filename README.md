# Donor Tools Java Client

donor-tools-api-java provides a Java client for the Donor Tools (donortools.com) API

## Usage

Add the following Maven dependency:

```xml
<dependency>
    <groupId>org.threeriverdev</groupId>
    <artifactId>donor-tools-api-java</artifactId>
    <version>1.0.0.Final</version>
</dependency>
```

Code example:

```java
import org.threeriverdev.donortools.*;

...

DonorToolsClient client = new DonorToolsClient("https://[USERNAME].donortools.com", "username", "password");

// create Persona

Persona persona = new Persona();
Persona.Name name = new Persona.Name(firstName, lastName);
persona.addName(name);

Persona.Address address = new Persona.Address();
address.setStreetAddress(streetAddress);
address.setCity(city);
address.setState(state);
address.setPostalCode(zip);
persona.addAddress(address);

Persona.EmailAddress emailAddress = new Persona.EmailAddress(email);
persona.addEmailAddress(emailAddress);

personaId = donorToolsClient.create(persona);

// store the personaId for re-use

// create Donation

Donation donation = new Donation();

donation.setDonationTypeId(14); // Donor Tools built-in donation type: Online Donation
donation.setPersonaId(personaId);
donation.setSourceId(sourceId);
donation.setAmountInCents(amountInCents);
donation.setMemo("This is a test.");

// Splits allow you to split a single donation up into multiple target funds.
Donation.Split split = new Donation.Split();
split.setAmountInCents(splitAmountInCents);
split.setFundId(fundId);
donation.addSplit(split);

donorToolsClient.create(donation);

// list all Personas
List<Persona> personas = client.listPersonas();
```

## How to Deploy a Snapshot

1. Add the following to ~/.m2/settings.xml
```xml
<server>
  <id>ossrh</id>
  ***REMOVED***
  ***REMOVED***
</server>
```
2. mvn clean deploy

## How to Deploy a Release

1. Add the following to ~/.m2/settings.xml
```xml
<server>
  <id>ossrh</id>
  ***REMOVED***
  ***REMOVED***
</server>
```
2. mvn versions:set -DnewVersion=1.2.3.Final
3. git add .
4. git commit -m "1.2.3.Final release"
5. git tag 1.2.3.Final
6. mvn clean deploy -P release
7. mvn versions:set -DnewVersion=1.2.4-SNAPSHOT
8. git add .
9. git commit -m "1.2.4-SNAPSHOT"
10. git push origin master 1.2.3.Final

## License

Licensed under the GNU LESSER GENERAL PUBLIC LICENSE (LGPL) V3.  See lgpl-3.0.txt for more information.