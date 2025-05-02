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

I have started researching how a rhythm game would work within UE5 opting to use C++ to maximise the learning possible within the confines of the project. After some research (https://www.youtube.com/watch?v=FgR35xDWbw4 and https://www.youtube.com/watch?v=F0PFHXUfa2Y among others) found that the best solution was to synchronise the code with the music through events trigerred in a level sequence, opting to keep it simple I had seperate events to open and close the hit window for each note however to impliment it fully I will change it to one event which opens and closes the window itself so that the gap can be consistent and I can make it modular for difficulty settings. I found most of the documentation I need is hidden away which is where forums like r/unrealengine and stack overflow are valuable resources, this is exactly how I came across this method of doing things with a clear explanation as to why (with enough time spent in the comments).

Coding Club: Maths and Logic Primer

This session of the club was extroadinarily helpful when it comes to my general understanding of how games work behind the seams, as such I have taken extensive notes of practical formulae which I may in the future build into a maths library of my own that focuses on relevant functions for game dev. it covered such things as methods of reading a 1 dimensional array as if it were 2 dimensional, how the modulo of a random number will end up biased unless you use a factor of the range for the modulo operation, euler angles vs radians, how square root functions are expensive, look at angles can be found using the change in y over change in x in the ATan2 function, how convert a theoretical movement on an angle into a usable change in x and y (and by extention vice versa), how a linear interpolation works, some logic gates, and how short circuit detection can allow for optimisation of logical evaluation. I am certain that I will end up using all of these as I continue this year. 

consolidation week

over the consolidation week i have worked extensively on the second game jam "shoot 'em up" where the teaching I have received already has been invaluable, not just for bug fixing in the discord but the additional coding for cool kids club, what was posed as a solution for radial menu's (ATan2) came in handy for creating the aiming for a twin stick style shooter:

```
FRotator ALightsCameraActionCharacter::GetAimRotation()
{
	// finds mouse position in viewport
	float MouseX;
	float MouseY;
	UGameplayStatics::GetPlayerController(GetWorld(), 0)->GetMousePosition(MouseX, MouseY);
	
	// finds radians and angle of mouse from the centre of screen
	float AimRadians = atan2((MouseY-ViewportCenter.Y), (MouseX-ViewportCenter.X));
	FRotator AimRotation = FRotator(0.f, (AimRadians*180/PI)+90, 0);

	// makes the aim rotation the same notation as the component rotation (-180 to 180)
	if (AimRotation.Yaw > 180)
	{
		AimRotation.Yaw -= 360;
	}
	
	return AimRotation;
}
```
however I did have to adjust one rotation to match the other so that they both operated in the same range of values, -180 to 180 as opposed to -90 to 270 or 0 to 360.

Another thing that has become more and more routine since the I was introduced to it is considering how logical expressions can take advantage of short circuit detection to minorly improve the efficiency of my code.

In addition to the maths and logic coming in handy I am starting to become more familiar with both C++ and Unreal Engine's implimentation of it leading to fewer build errors and move onto the standard bugs quicker speeding up my C++ development massively particularly for the simpler more standard features such as input and additional components in a character.

Shader Programming

in my spare time between game jams I have been independently experimenting with HLSL, Unity's shader language creating several post-processing effects like dithering and a greyscale filter this has been a fascinating dive into how meshes become images and has introduced me to several concepts which will be useful when working with floats such as quantization and methods of modifying a 0 - 1 range into other ranges like -1 - 1. using the shader programming youtube channel Acerola as inspiration and Freja Holmes' youtube tutorials on Unity shaders to inform how I impliment them, I now have many functional colour correction and stylistic effects including cell shading, dithering, brightness and exposure.

Coding Club: Debugging - Practice of Programming

once again I found Myself taking extensive notes during this session although this time they are more reminders to myself as many times the most successful approach to debugging is the one where you consider yourself an idiot and find the one place that it rings true, these notes include such wisdoms as: analyse the problem properly before you try to change any code, take breaks they help I promise, check for the most simple problems first a rogue semicolon can spell your doom even after many years in the industry. then came more practical steps that may simplify the bug hunt such as: testing in isolation - if it worked last time what did you change? or if you have a function can you test it with manual input and output? only change one thing at a time, should you find a mistake check for where else you may have made it to save future headaches, magic numbers can be forgotten so it is best to set them as constants using features like #define, defining edge cases allows you to manually work out what a portion of your code should do, and if you can replicate the bug then you can vary the method used to induce it and isolate the cause. we also raised awareness of possible likely scenarios that could break code like: negative numbers, zero, or powers of 2. Graphs can be a great tool to viualise when something breaks and it can be a good idea to keep record of how these results change when you change each part of the code. These are all meaningful steps that join rubber ducking in my arsenal and will hopefully become subconscious habit.

Unity

To be able to create the best final product possible for game jam 3 I am learning unity for 2D games, and as such I am realising how similar it is to unreal engine with most if not all functions having direct equivalents as well as C++ and C# being Identical for every application I have had for them so far. As well as a crash course in unity this game jam serves as an opportunity to begin putting into practice a lot more "designer friendly" coding where I attempt to make as much as possible easy to tweak in the unity editor itself by serialising fields. I am also able to experience developing as a team and actually use some more source control features now that I have another programmer to work with (although it seems i am doing almost all of the work). Through Game Jam 3 I found that much of Unity's documentation is easier to follow than unreal meaning i have spent less time in forums and more time in documentation for the research that led to the final product.

Coding Club: Recursion

in this session we covered recursion, the stack overflow error and ways to create non recursive versions of recursive functions to prevent such errors. Recursion is a practise I have encountered before and utilised unaware of the issues it can cause, because of this I paid extra attention and came away with valuable knowledge of steps to break down a recursive function often involving keeping a track of data that would normally be kept in the scope of each layer of recursion and implementing the repeated behaviour through a while loop. it was also noted that it is typically best to start by defining some exit conditions where the recursive function would stop and working backwards compared to how you would implement the behaviour recursively.

Code Studio Tasks

throughout the code studio tasks I have found it quite simple to convert my knowledge of other languages to C++ however pointers are a new concept for me, through task 7 I was able to complete the workshop but was left confused as to the purpose of pointers beyond pass by reference that was until I did a quick google search and found several posts detailing the heap vs the free store, this not only helped cement the pointers knowledge in task 7 but prepare me better for task 8, this also lead to many posts about the speed differences between the 2 giving me a better understanding of how to optimise my code in the future.

GGJ and the final Game Jam

Beginning with the global game jam, I explored Unreal Engine's AI systems for enemies in the most basic way possible to get enemies to target different things to attack, given the 5 day time constraint the fact that the game functioned while i was actively learning this new tool is a success. Then came the final game jam, the group picked Don't Duck Around, another project which required an AI however this time in Unity so that I could leverage the graphics programming I had done in unity to create a custom cell shader. For this i have constructed a Finite State Machine to be the underlying system that manages the Duck's Behaviour, this involved significant research into finite state machines themselves as well as methods of creating a timed repeating effect in unity I settled on a coroutine. Here is the code for the current version of the Finite State Machine and base State class as of 18/02/25:

```
public class FiniteStateMachine : MonoBehaviour
{
    private List<State> availableStates = new List<State>();
    
    private void Start()
    {
        // when the duck starts it moves into an idle state which acts as a break glass in emergency state from which the duck restarts its decisions
        
        availableStates.Add(this.AddComponent<State_Idle>());
        availableStates.Add(this.AddComponent<State_Test>());
        
        StartIdleState();
    }

    void StartIdleState()
    {
        foreach (State state in availableStates)
        {
            if (state.GetType() == typeof(State_Idle))
            {
                // entering or activating a state requires a reference to the state machine which is used to call the exit function and an array of all states so that the state can select the exit condition
                state.Activate(this, availableStates);
            }
        }
    }

    public void ExitFromState(State NextState)
    {
        // the duck will never not be in a state so exiting one state and starting a new one are the same thing
        
        NextState.Activate(this, availableStates);
    }
    
}
```
```
public class State : MonoBehaviour
{
    protected FiniteStateMachine stateMachine;
    protected List<State> availableStates;
    
    /* states will activate by gathering necessary data, at minimum this is the machine that called it and an array of available states
     * once all data is known it transitions into the state loop where it does its task and periodically checks if exit conditions have been met
     * essentially bouncing between the state loop and check exit conditions function
     * when an exit condition is met it calls exit which tells the state machine which state to use next
     */
    
    public virtual void Activate(FiniteStateMachine CallingStateMachine, List<State> AvailableStates)
    {
        stateMachine = CallingStateMachine;
        availableStates = AvailableStates;

        State ExitCondition = null;
        StartCoroutine(StateLoop(ExitCondition));
    }

    protected virtual IEnumerator StateLoop(State ExitCondition)
    {
        
        while (!ExitCondition)
        {
            // do something
        
            ExitCondition = CheckExitCondiditons();

            yield return new WaitForSeconds(0.2f);
        }
        
        Exit(ExitCondition);
    }

    protected virtual State CheckExitCondiditons()
    {
        // if condition met return state to transition to
        return availableStates[0];
    }

    protected virtual void Exit(State ConditionMet)
    {
        stateMachine.ExitFromState(ConditionMet);
    }
}
```
as you can see the State class is commented in such a way that it acts as both template and guide for creating future states which should also keep me working consistently across all states.

CSGO Artefact

For My CSGO artefact I decided to create a bullet hell game which used manipulation of time as its core mechanic. To spawn the masses of projectiles I created a spawner and spawn pattern manager which adresses arrays of references to spawners added from the level

![image](https://github.com/user-attachments/assets/abf42ce4-f583-423f-8148-01532a532cb6)

each spawner has spawning functions that target different locations such as the player or a specified location or to the opposite direction, most of this was basic stuff that both i had done before and then was covered in the workshop tasks however what was new was using a level sequence to issue the commands to the manager so that they can be plotted out in actual time which is also effected by the time dilation.
it looks something like this : 

![image](https://github.com/user-attachments/assets/b2f347cd-210d-4001-a9fe-71c1e62ab39b)

This will prove to be a useful tool moving forwards when functions require a time based sequencing, and it was also one that took very little research to figure out with very few bugs along the way.

Creating the manipulation of time was a good case study into how game engines implement certain features that perform actions over time such as timelines and timers since they were each affected by the time dilation. What took up a lot of the development time was figuring out that I had to map the linear input of the scroll wheel to a non linear effect, since 0.2-1 has the same effect as 1-5 my solution was to adjust the input by using it as the exponent to a dilation constant before changing the values with the following function : 

![image](https://github.com/user-attachments/assets/af1554cd-f230-4998-95c5-96a7484895a1)

Finite State Machine Optimisations

I was watching youtube and came across someone talking about Finite State Machines, having made my own without looking at any sort of guide I decided to look at their implementation (https://youtu.be/r-RCfmQqLA0?t=766) and instantly felt like an idiot for not instantiating the different states rather than passing a hash set of possible states around. the next day I re-wrote both the state machine and state classes to look like this:
```
public class FiniteStateMachine : MonoBehaviour
{
    private State activeState = new State_Idle();

    public NavMeshAgent _agent;

    private void Start()
    {
        _agent = GetComponent<NavMeshAgent>();

        StartCoroutine(MachineLoop());
    }
    
    
    private IEnumerator MachineLoop()
    {
        while(Application.isPlaying)
        {
            activeState = activeState.StateAction(this);

            yield return new WaitForSeconds(0.2f);
        }
    }
}

```

```
public class State
{
    protected FiniteStateMachine stateMachine;

    public virtual State StateAction(FiniteStateMachine StateMachine)
    {
        stateMachine = StateMachine;
        
        //Do a thing
        
        // maybe wait some time
        
        return new State();
    }
}
```
I also want to look at making this asynchronous to divorce it from the main thread and allow me to put the AI on a more reasonable loop rather than the coroutine that I am using at the moment.

Coding Club - Programming Tricks we got from AI

This session covered both how Large Language models like chat GPT are really bad at coding for anything but low complexity generic problems since it regurgitates information from its training data, which also means that it is outdated constantly. the session then moved on to other forms of AI and how creating these systems has tought us valuable lessons like how blurring the lines between functions and data can lead to incredibly elegant solutions like complex event systems as well as how it lead to languages like perl for registry expressions and the efficiency that brings in sorting masses of data based soley on patterns. This talk also valuably gave me an insight into A star searches in data trees and how it avoids the pitfalls of depth first and breadth first searching particularly in data structures without a defined end. At some point I would like to dig into the actual code behind A star but that will be saved for another time.

Navigation/Interaction AI

This is likely the most complex piece of code I have ever written; This class is the Navigation state for the finite state machine I created for the game jam; it handles most of the duck's decision making and calls to the navmesh agent. This is the translation of the chance-based behaviours my designer laid out here:

Action object in duck radius?
Peaceful interactable 40% chance to interact
Pickupable item 40% chance to pick up
Every 10s held in mouth 20% more likely to attempt to swallow if swallowable & if not interacted with/swallow 10% more likely to drop
After interaction ban on interaction with same object for 45s
30% to do death interaction with object
Is object breakable? 30% to peck. Every peck 40% more likely to peck again. Object initially has 30% chance to break. After every peck object is 20% more likely to break
If no interactable objects around 10% chance to sleep for 10-15 seconds(+ an extra 5% if near something that gives off heat or carpet) 90% chance to scan for the nearest interact able object in ducks vicinity and move towards it.

which I then made sense of in MS paint
![AI plan - Organised](https://github.com/user-attachments/assets/fd6c9e09-133b-49b9-a4ea-e9b591ee404a)


```
public class State_Navigation : State
{
    
    private NavMeshAgent _agent;

    private float objectRange = 25;

    public override State StateAction(FiniteStateMachine StateMachine)
    {
        stateMachine = StateMachine;
        _agent = stateMachine._agent;
        
        if (!_agent) {return new State_Idle();}

       
        if (!_agent.isOnNavMesh)
        {
            return new State_Idle();
        }
        
        if (!_agent.hasPath || _agent.isPathStale)
        {
            NavDecisionTree();
        }
        
        return new State_Idle();
        
    }

    private State Nav_ItemInRange(List<InteractableObject> objects)
    {
        int roll = Random.Range(1, 10);

        if (roll <= 4)
        {
            InteractableObject interactableObject = GetRandomInteractableObjectWithTag(objects, "peaceful");
            
            if (interactableObject)
            {
                _agent.SetDestination(interactableObject.transform.position);

                State_Interaction interact = new State_Interaction();

                interact.TargetObject = interactableObject;
                
                return interact;
            }
            
            return new State_Idle();
        }
        if (roll <= 8)
        {
            InteractableObject interactableObject = GetRandomInteractableObjectWithTag(objects, "harmful");
            
            if (interactableObject)
            {
                _agent.SetDestination(interactableObject.transform.position);

                State_Interaction interact = new State_Interaction();

                interact.TargetObject = interactableObject;
                
                return interact;
            }
            
            return new State_Idle();
        }
        else
        {
            _agent.SetDestination(stateMachine.transform.position + new Vector3(Random.Range(-25, 25), Random.Range(-25, 25), Random.Range(-25, 25)));
        }

        return new State_Idle();
    }

    private State Nav_NoneInRange(InteractableObject interactableObject)
    {
        if (Random.Range(1, 10) == 1)
        {
            State_Sleep sleep = new State_Sleep();

            sleep.Repetitions = 30;
            
            return sleep;
        }
        
        _agent.SetDestination(interactableObject.transform.position);
        
        State_Interaction interact = new State_Interaction();

        interact.TargetObject = interactableObject;
        
        return interact;
    }

    private InteractableObject GetRandomInteractableObjectWithTag(List<InteractableObject> objects, string tag)
    {
        objects.TrimExcess();
        
        List<InteractableObject> objectsCopy = new List<InteractableObject>(objects);
        foreach (InteractableObject i in objectsCopy)
        {
            if (!i.gameObject.CompareTag(tag))
            {
                objects.Remove(i);
                
                continue;
            }

            if (i.onCooldown)
            {
                objects.Remove(i);
            }
        }

        int count = objects.Count;

        if (count == 0)
        {
            return null;
        }

        return objects[Random.Range(0, count - 1)];
    }

    private void NavDecisionTree()
    {
        InteractableObject[] interactableObjects = Object.FindObjectsByType<InteractableObject>(FindObjectsInactive.Exclude, FindObjectsSortMode.None);

        float LowestDistance = objectRange * 60;
        
        InteractableObject closestObjectInRange = null;
        InteractableObject closestObject = null;
        
        List<InteractableObject> ObjectsInRange = new List<InteractableObject>();
        
        foreach (InteractableObject interactableObject in interactableObjects)
        {
            if (interactableObject.onCooldown)
            {
                continue;
            }
            
            float distanceToObjectSquared = absolute_Difference2D(interactableObject.transform.position, stateMachine.transform.position).sqrMagnitude;
            
            if (distanceToObjectSquared < LowestDistance)
            {
                LowestDistance = distanceToObjectSquared;
                
                closestObject = interactableObject;

                if (LowestDistance < objectRange)
                {
                    closestObjectInRange = interactableObject;
                }
            }

            if (distanceToObjectSquared < objectRange)
            {
                ObjectsInRange.Add(interactableObject);
            }
            
        }

        if (closestObject == closestObjectInRange)
        {
            Nav_ItemInRange(ObjectsInRange);
        }
        else if (closestObject)
        {
            Nav_NoneInRange(closestObject);
        }
    }

    private Vector2 absolute_Difference2D(Vector3 a, Vector3 b)
    {
        return new Vector2(Mathf.Abs(Mathf.Abs(a.x) - Mathf.Abs(b.x)), Mathf.Abs(Mathf.Abs(a.z) - Mathf.Abs(b.z)));
    }
    
}
```

Remarkably, almost everything worked the first time. I had one small issue where the tag filtering didn't seem to work. It took some time, but eventually, I figured out that the compare tag function only compares the object that contains the script, not the entire hierarchy. I had tagged objects further up the hierarchy. To fix this, it was a simple case of tagging the individual interactable, which has the added benefit of allowing multiple interactables on the same object. Parts of the designer's intent are still not finished as of writing, but this covers the vast majority of it; the rest will be quite simple in comparison.
