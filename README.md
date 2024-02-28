# meetings
<code><p>
package com.infy.meeting.entity;
@Entity
@Table(name="meeting")
public class Meeting {
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  private Integer meetingId;

  DTO
 meetingDTO.java
 package com.infy.meeting.dto;
 @NotNull(message="{SchedulerName.INVALID}")
 @Pattern(regexp = "[a-zA-Z\s]+", message="{Scheduler>Name.Invalid}")
 private String schedulerName;

 @NotNull(message="{Team.Name.INVALID}")
 private String teamName;

 @NotNull(message="{Purpose.INVALID}")
 private String purpose;

 //MeetingApplication.java
 package com.infy.meeting;

 @SpringBootAplication
 public class MeetingAplication {
   public static void main(String[] args) {
   SringApplication.run(MeetingApplication.class, args);
   }
}
 
  </code></p>
  
  
