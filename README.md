# meetings
<code><p>
package com.infy.meeting.entity;
@Entity
@Table(name="meeting")
public class Meeting {
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  private Integer meetingId;

 <b> DTO-----></b>
 meetingDTO.java
 package com.infy.meeting.dto;
 @NotNull(message="{SchedulerName.INVALID}")
 @Pattern(regexp = "[a-zA-Z\s]+", message="{Scheduler>Name.Invalid}")
 private String schedulerName;

 @NotNull(message="{Team.Name.INVALID}")
 private String teamName;

 @NotNull(message="{Purpose.INVALID}")
 private String purpose;

 <b>MeetingApplication.java-------></b>
 package com.infy.meeting;

 @SpringBootAplication
 public class MeetingAplication {
   public static void main(String[] args) {
   SringApplication.run(MeetingApplication.class, args);
   }
}
 <b>MeetingAPI.java------></b>
 import java.utli.List;
 @RestController
 @RequestMapping(vallue="/api")
 @validated
 public class MettingAPI {
   @Autowired
   private Meetingservice meetingser;

   @GetMapping(value="/meeting/{schedulerName}")
   public ResponseEntity<*List<*MeetingDTO*>*> getAllMeetingScheduler(@PathVariable String schedulerName)
   throws MeetingException{
   List<MeetingDTO> meetingDTO=meetingser.getAllMeetingOfScheduler(schedulerName);
   return new ResponseEntity<>(meetingDTO,HttpStatus.OK);
}
@PostMapping(value="meeting")
public ResponseEntity<*MeetingDTO*> schedulerMeeting( @Valid @RequestBody MeetingDTO meetingDTO)
throws MeetingException{
  MeetingDTO meetingDTO1 =meetingser.scheduleMeeting(meetingDTO);
  return new ResponseEntity<>(meetingDTO1,HttpStatus.CREATED);
  }
}
<b> Meeting Exception------></b>
package com.infy.meeting.exception;
public class MeetingException extends Exception {
  private static final long serialVersionUID = 1L;

  public MeetingException(String message) {
    super(message);
    }
  }

<b> MeetingServiceimpl.java-----></b>
package com.infy.meeting.service;
...
@Service(value="/meetingService")
public class MeetingServiceImp1 implements Meetingservice{
  @Autowired
  private MeetingRepository meetingRepo;
@Override
public List<*MeetingDTO*> getAllMeetingOfScheduler(String schedulerName) throws MeetingException {
list<*Meeting*> meeting=meetingRepo.getMeetingBySchedulerName(schedulerName);
if(meeting.isEmpty()|| meeting.size()==0 {
  throw new MeetingException("MeetingService.NO.MEETING.FOUND");
  }
   
...
@Override
....
..
<b>Meeting Utility Exception----></b>
import com.infy.meeting.exception.MeetingException;
@RestControllerAdvice
public class ExceptionControllerAdvice {
  @Autowired
  Environment environment;

  @ExceptionHandler(Exception.class)
  public ResponseEntity<*ErrorInfo*> exceptionHandler(Exception exception) {
  ....
  ..
  @ExceptionHandler(MeetingException.class)
  public ResponseEntity<*ErrorInfo*> MeetingExceptionHandler( MettingException exception)
    ErrorInfo error = new ErrorInfo();

<b>ExceptionCo</b>
@ExceptionHandler(Exception.class)
public ResponseEntity<*ErrorInfo*> exceptionHandler(Exception exception) {
..
@ExceptionHandler(MeetingException.class)
public ResponseEntity<*ErrorInfo*> MeetingExceptionHandler( MeetingException Exception){
...
@ExceptionHAndler(MethodArgumentNotValidException.class)
public Respomseaentity<*ErrorInfo*> exceptionHandler(MethodArgumentNotValidException exception) {
......
<b>LoggingAspec------></b>
package com.infy.meeting.utility;
..
@Component
@Aspect
public class LoggingAspect {
   public static final log LOGGER = LogFactory.getLog(loggingAspect.class);
...
  @AfterThrowing(pointcut = "execution(* com.infy.meeting.service.*Imp1.*(..))", throwing = "exception")
  public void logServiceExecption(Exception execption) throws Exception {
      LOGGER.error(exception.getMessage(),exception;
      }
   }   
   <b>Meeting validator---></b>
   import java.time.localDate;
   import com.infy.meeting.dto.meetingDTO;
   import com.infy.meeting.exception.MeetingException;
   public class MeetingValidator {
     public staic void validateMeeting(meetingDTO meetingDTO) throws MeetingException {
       if(! is ValidTeamName(meetingDto.getTeamName())){
           throw new MeetingException("MeetingValidator.IVALID_TEAM_NAME");
        }
        if(! is ValidMeetingdate(meetingDto.getMeetingDate())){
           throw new MeetingException("MeetingValidator.INVALID_MEETING_DATE");
          }
      }
      Public static boolean isValidTeamName(String teamName){
      if (teamName.equals("ETAMYSJAVA")||teamName.equals("ETAMYSUI")||teamName.equals("ETAMYSBI")||teamName.equals("ETAMYSMS")
|| teamName.equals("ETAMYSAI")){
     return true;
    }else
      return false;
}
         Public static boolean isValidMeetingDate(LocalDate meetingDate){
         DayOfWeek dayOfWeek = meetingDate.getDayOfWeek();
         if(DayOfWeek.SATURDAY.equals(dayOfWeek) || DayOfWeek.SUNDAY.equals(dayOfWeek)){
            return false;
            }else
              return true;


      }
             
  </code></p>
  

