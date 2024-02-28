# meetings
package com.infy.meeting.entity;

@Entity
@Table(name="meeting")
public class Meeting {
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  private Integer meetingId;
  
  
