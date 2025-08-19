 enumerations required in the car rental system. According to the class diagram, seven enumerations are used in the system, 
 i.e., VehicleStatus, AccountStatus, ReservationStatus, PaymentStatus, VanType, CarType, and VehicleLogType.


//======
public enum MotorcycleType {
    STANDARD, CRUISER, TOURING, SPORTS, OFF_ROAD, DUAL_PURPOSE
}

public enum AccountStatus {
    ACTIVE, CLOSED, CANCELED, BLACKLISTED, BLOCKED
}

public enum ReservationStatus {
    ACTIVE, PENDING, CONFIRMED, COMPLETED, CANCELED
}

public enum PaymentStatus {
    UNPAID, PENDING, COMPLETED, CANCELED, REFUNDED
}

public enum VanType {
    PASSENGER, CARGO
}

public enum CarType {
    ECONOMY, COMPACT, INTERMEDIATE, STANDARD, FULL_SIZE, PREMIUM, LUXURY
}

public enum MotorcycleType {
    STANDARD, CRUISER, TOURING, SPORTS, OFF_ROAD, DUAL_PURPOSE
}

public enum TruckType {
    LIGHT_DUTY, MEDIUM_DUTY, HEAVY_DUTY
}

public enum VehicleLogType {
    ACCIDENT, FUELING, CLEANING_SERVICE, OIL_CHANGE, REPAIR, OTHER
}


//=======================
public class Address {
    private String streetAddress;
    private String city;
    private String state;
    private int zipCode;
    private String country;

    public Address(String street, String city, String state, int zip, String country) {
        this.streetAddress = street;
        this.city = city;
        this.state = state;
        this.zipCode = zip;
        this.country = country;
    }
    // Getters...
}

public abstract class Person {
    private String name;
    private Address address;
    private String email;
    private String phoneNumber;

    // Setters & getters...
}

public class Driver extends Person {
    private int driverId;
    // Setters/getters...
}
