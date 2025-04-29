
Use case diagram

![image](https://github.com/user-attachments/assets/b37a5038-6d39-4257-b398-cdc9546d1250)


public class User {
  private String name;
  private String email;
  public void respondInvitation(Notification invite);
}

public class MeetingRoom {
  private int id;
  private int capacity;
  private boolean isAvailable;
  private List<Interval> bookedIntervals;
}




public class Calendar {
  private List<Meeting> meetings;
}


public class Meeting {
  private int id;
  private int participantsCount;
  private List<User> participants;
  private Interval interval;
  private MeetingRoom room;
  private String subject
  
  public void addParticipants(List<User> participants);
}



public class MeetingScheduler {
  private User organizer;
  private Calendar calendar;
  private List<MeetingRoom> rooms;

  // Scheduler is a singleton class that ensures it will have only one active instance at a time
  private static MeetingScheduler scheduler = null;
    
  // Created a static method to access the singleton instance of Scheduler class
  public static MeetingScheduler getInstance() {
    if (scheduler == null) {
      scheduler = new MeetingScheduler();
    }
    return scheduler;
  }  

  public boolean scheduleMeeting(List<User> users, Interval interval);
  public boolean cancelMeeting(List<User> users, Interval interval);
  public boolean bookRoom(MeetingRoom room, int numberOfPersons, Interval interval);
  public boolean releaseRoom(MeetingRoom room, Interval interval);
  public MeetingRoom checkRoomsAvailability(int numberOfPersons, Interval interval);
}

public class Notification {
  private int notificationId;
  private string content;
  private Date creationDate;

  public boolean sendNotification(User user);
  public boolean cancelNotification(User user);
}


