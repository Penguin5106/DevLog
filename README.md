# CodeStudioDevLog_Year1

# TODO: Delete this information when it is practiced enough to become useless
The purpose of this devlog is to form the assessment submission for my Code Studio module. It must be reflective rather than descriptive, and it will be marked according to this grading scale:
![image](https://github.com/user-attachments/assets/d6b3b1af-2c1e-4889-a8b5-8185159ba1ac)


after looking at the reflective writing example it appears to follow this structure

1 research and methodology followed when approaching the task

2 problems that appeared (only major problems not i couldnt find the documentation), highlight where the research differs from reality

3 methodology of fixing the issue along with any data and research to support

4 what went well/wrong in both your original approach and how you fixed any issues

5 how would you handle this next time based on what you have learned

6 reference list

# DevLog Start

I have started researching how a rhythm game would work within UE5 opting to use C++ to maximise the learning possible within the confines of the project. After some research (https://www.youtube.com/watch?v=FgR35xDWbw4 and https://www.youtube.com/watch?v=F0PFHXUfa2Y among others) found that the best solution was to synchronise the code with the music through events trigerred in a level sequence, opting to keep it simple I had seperate events to open and close the hit window for each note however to impliment it fully I will change it to one event which opens and closes the window itself so that the gap can be consistent and I can make it modeular for difficulty settings. I found most of the documentation I need is hidden away which is where forums like r/unrealengine and stack overflow are valuable resources.
