# TRAFFIC SIGNAL SIMULATOR WITH CIRCULAR QUEUE
## Data Structures and Algorithms Course Project

---

## FRONT PAGE

**Vellore Institute of Technology**  
*(Deemed to be University under section 3 of UGC Act, 1956)*

**SCHOOL OF COMPUTER SCIENCE AND INFORMATION SYSTEMS**  
**FALL SEMESTER 2025-26**

---

**Course Code:** ISWE102L  
**Course Name:** Data Structures and Algorithms  
**Slot:** B1+TB1  
**Faculty:** Dr Yoga Raja C A

---

### Course Project Team

| S.No | Name      | Register Number |
|------|-----------|-----------------|
| 1.   | Vaishali B| 24MIS0378       |
| 2.   | Kanishka  | 24MIS0314       |
| 3.   | Keerthana | 24MIS0192       |

---

**Project Title:** Traffic Signal Simulator with Circular Queue

**Date Submitted:** October 30, 2025

---

## ABSTRACT

This project presents a **Traffic Signal Simulator** that demonstrates the practical application of a **Circular Queue** data structure in managing vehicle flow at a traffic intersection. The system simulates real-world traffic control where cars arrive at a signal and are processed based on the traffic light state. 

The simulator uses a circular queue to efficiently manage vehicles in a fixed-capacity queue with wrap-around functionality. When the traffic light is red, cars are automatically enqueued (added to the queue). When the light turns green, cars are dequeued (removed from the queue) in FIFO (First-In-First-Out) order. The yellow light serves as a transition state between red and green.

Visual animations and real-time status updates make queue operations clear and engaging. The system includes manual controls for enqueue/dequeue operations, adjustable simulation speed, dynamic queue resizing (4-16 slots), and comprehensive operation logging. Overflow and underflow conditions are handled gracefully with toast notifications.

The project connects theoretical DSA concepts to a practical urban traffic management scenario, providing an interactive learning experience that bridges the gap between theory and real-world applications.

---

## DATA STRUCTURE USED

### Primary Data Structure: **CIRCULAR QUEUE**

A **circular queue** is an advanced linear data structure where the last position is connected back to the first position to form a circle. This implementation overcomes the limitations of a simple linear queue by reusing empty spaces created after dequeue operations.

#### Key Components:

1. **Queue Array**: Fixed-size array storing car IDs (nullable integers)
2. **Front Pointer**: Tracks the position of the first element to be dequeued
3. **Rear Pointer**: Tracks the position where the next element will be enqueued
4. **Size Counter**: Current number of elements in the queue
5. **Max Size**: Total capacity (configurable from 4 to 16 slots)

#### Circular Nature:

When the rear pointer reaches the end of the array and there's space at the beginning, it wraps around to index 0. This is achieved using the modulo operation:

```
newRear = (rear + 1) % maxSize
```

This wrap-around mechanism allows efficient space utilization without wasting memory.

#### Queue States:

- **Empty Queue**: `size = 0`, `front = 0`, `rear = -1`
- **Partially Filled**: `0 < size < maxSize`
- **Full Queue**: `size = maxSize`

#### Advantages of Circular Queue:

1. **Space Efficiency**: Reuses empty spaces after dequeue operations
2. **Fixed Memory**: No dynamic memory allocation required
3. **Constant Time Operations**: Both enqueue and dequeue are O(1)
4. **No Shifting**: Unlike linear queues, no element shifting needed

---

## OPERATIONS

### Core Queue Operations

#### 1. **ENQUEUE (Add Car)**
- **Description**: Adds a new car to the rear position of the queue
- **When**: Automatically triggered during RED light phase
- **Prerequisites**: Queue must not be full (`size < maxSize`)
- **Steps**:
  1. Check if queue is full
  2. Calculate new rear position: `rear = (rear + 1) % maxSize`
  3. Insert car ID at `queue[rear]`
  4. Increment size counter
  5. Log operation with timestamp
- **Time Complexity**: O(1)
- **Visual Feedback**: Car icon (🚗) appears with fade-in animation

#### 2. **DEQUEUE (Remove Car)**
- **Description**: Removes car from the front position of the queue
- **When**: Automatically triggered during GREEN light phase
- **Prerequisites**: Queue must not be empty (`size > 0`)
- **Steps**:
  1. Check if queue is empty
  2. Retrieve car ID from `queue[front]`
  3. Set `queue[front]` to null
  4. Update front: `front = (front + 1) % maxSize`
  5. Decrement size counter
  6. Log operation with timestamp
- **Time Complexity**: O(1)
- **Visual Feedback**: Car icon fades out from slot

#### 3. **OVERFLOW CHECK**
- **Description**: Prevents enqueue when queue is at maximum capacity
- **Condition**: `size == maxSize`
- **Action**: Display toast notification "Queue is full!"
- **Time Complexity**: O(1)

#### 4. **UNDERFLOW CHECK**
- **Description**: Prevents dequeue when queue is empty
- **Condition**: `size == 0`
- **Action**: Display toast notification "Queue is empty!"
- **Time Complexity**: O(1)

#### 5. **RESET**
- **Description**: Clears entire queue and resets to initial state
- **Steps**:
  1. Set all queue slots to null
  2. Reset front = 0, rear = -1
  3. Reset size = 0
  4. Clear operation log
  5. Stop simulation
- **Time Complexity**: O(1)

#### 6. **RESIZE QUEUE**
- **Description**: Changes queue capacity (4-16 slots)
- **Action**: Resets queue and applies new size
- **Time Complexity**: O(n) where n is the new size

#### 7. **TRAFFIC LIGHT CYCLE**
- **State Transitions**: RED → YELLOW → GREEN → RED
- **RED Phase**: 3 seconds (enqueue operations)
- **YELLOW Phase**: 1 second (transition only)
- **GREEN Phase**: 3 seconds (dequeue operations)
- **Time Complexity**: O(1) per state change

---

## TECHNOLOGY USED

### Frontend Technologies

| Technology | Version | Purpose |
|------------|---------|---------|
| **React** | 18.3.1 | Component-based UI framework for building interactive interfaces |
| **TypeScript** | Latest | Static type checking for code reliability and better development experience |
| **Vite** | Latest | Fast build tool and development server with hot module replacement |

### Styling & Design

| Technology | Version | Purpose |
|------------|---------|---------|
| **Tailwind CSS** | Latest | Utility-first CSS framework for rapid UI development |
| **shadcn/ui** | Latest | Pre-built accessible components based on Radix UI |
| **Lucide React** | 0.462.0 | Modern icon library with scalable SVG icons |
| **Tailwind Animate** | 1.0.7 | Animation utilities for smooth transitions |

### State Management & Routing

| Technology | Version | Purpose |
|------------|---------|---------|
| **React Hooks** | Built-in | useState, useEffect, useCallback for local state management |
| **React Router DOM** | 6.30.1 | Client-side routing for single-page application navigation |

### UI Enhancement

| Technology | Version | Purpose |
|------------|---------|---------|
| **Sonner** | 1.7.4 | Toast notification system for user feedback |
| **Class Variance Authority** | 0.7.1 | Managing component variants and conditional classes |

### Development Tools

| Tool | Purpose |
|------|---------|
| **ESLint** | Code quality and consistency checking |
| **Git** | Version control system |
| **npm/bun** | Package management |

---

---

## User Interface Layout

```
┌─────────────────────────────────────────────────────┐
│          Traffic Signal Queue Simulator              │
│          (with Traffic Light Animation)              │
├─────────────────────────────────────────────────────┤
│                                                       │
│  ┌──────────┐    ┌───────────────────────────┐     │
│  │ Traffic  │    │   Circular Queue Grid      │     │
│  │  Light   │    │  [🚗] [ ] [🚗] [ ]         │     │
│  │          │    │  [🚗] [ ] [ ] [🚗]         │     │
│  │   ⬤ Red  │    │   Front ↓    Rear ↓       │     │
│  │   ⬤ Yellow│   └───────────────────────────┘     │
│  │   ⬤ Green│                                       │
│  └──────────┘    ┌───────────────────────────┐     │
│                   │ Status: Size 4 / 8        │     │
│                   │ Queue has space ✓         │     │
│  ┌───────────────┴───────────────────────────┘     │
│  │ Simulator Controls                              │
│  │ [▶ Start] [↻ Reset]                            │
│  │ Queue Size: [8] ━━━━○━━                        │
│  │ Speed: ━━━━○━━━ 1.0x                           │
│  │ [+ Enqueue] [- Dequeue]                        │
│  └─────────────────────────────────────────────────┤
│                                                       │
│  ┌─────────────────────────────────────────────────┐│
│  │ Operation Log                                    ││
│  │ 🟢 DEQUEUE: Car #12 - 10:35:42                  ││
│  │ 🔴 ENQUEUE: Car #13 - 10:35:40                  ││
│  │ 🟢 DEQUEUE: Car #11 - 10:35:38                  ││
│  └─────────────────────────────────────────────────┘│
│                                                       │
│  ┌─────────────────────────────────────────────────┐│
│  │ How It Works                                     ││
│  │ • Circular queue manages cars at intersection   ││
│  │ • Red light: cars enqueue (join queue)          ││
│  │ • Green light: cars dequeue (leave queue)       ││
│  └─────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────┘
```

---

## Algorithm & Implementation

### Enqueue Algorithm (Add Car)
```
ALGORITHM Enqueue(queue, rear, size, maxSize, carId):
  1. IF size == maxSize THEN
       DISPLAY "Queue is full!"
       RETURN false
  2. rear ← (rear + 1) MOD maxSize
  3. queue[rear] ← carId
  4. size ← size + 1
  5. LOG "ENQUEUE: Car #carId"
  6. RETURN true
```

### Dequeue Algorithm (Remove Car)
```
ALGORITHM Dequeue(queue, front, size, maxSize):
  1. IF size == 0 THEN
       DISPLAY "Queue is empty!"
       RETURN false
  2. carId ← queue[front]
  3. queue[front] ← null
  4. front ← (front + 1) MOD maxSize
  5. size ← size - 1
  6. LOG "DEQUEUE: Car #carId"
  7. RETURN true
```

### Traffic Light State Machine
```
ALGORITHM TrafficLightCycle():
  1. currentState ← RED
  2. WHILE simulation is running DO
       3. IF currentState == RED THEN
            4. WAIT 3 seconds
            5. TRY Enqueue() every 1 second
            6. currentState ← YELLOW
       7. ELSE IF currentState == YELLOW THEN
            8. WAIT 1 second
            9. currentState ← GREEN
       10. ELSE IF currentState == GREEN THEN
            11. WAIT 3 seconds
            12. TRY Dequeue() every 1 second
            13. currentState ← RED
```

---

## Component Architecture

### Main Components:

1. **Index.tsx** (Main Container)
   - Manages all state (queue, pointers, traffic light, logs)
   - Implements core queue operations
   - Controls traffic light cycle
   - Coordinates child components

2. **TrafficLight.tsx**
   - Displays three-light traffic signal
   - Visual feedback with glow effects
   - Smooth color transitions

3. **CircularQueueVisualizer.tsx**
   - Renders queue grid layout
   - Highlights front/rear pointers
   - Shows car icons in occupied slots
   - Displays status information

4. **SimulatorControls.tsx**
   - Play/Pause button
   - Reset button
   - Speed slider
   - Queue size input
   - Manual enqueue/dequeue buttons

5. **OperationLog.tsx**
   - Displays operation history
   - Color-coded log entries
   - Scrollable container
   - Timestamp formatting

---

## Design System

### Color Palette (HSL Values)
- **Background**: `hsl(222, 47%, 11%)` - Dark blue-gray
- **Foreground**: `hsl(210, 40%, 98%)` - Off-white
- **Primary (Green Light)**: `hsl(142, 76%, 36%)` - Emerald green
- **Secondary (Yellow Light)**: `hsl(48, 96%, 53%)` - Bright yellow
- **Destructive (Red Light)**: `hsl(0, 72%, 51%)` - Signal red
- **Card Background**: `hsl(217, 33%, 17%)` - Slate
- **Border**: `hsl(217, 33%, 25%)` - Lighter slate

### Typography
- Font Family: System font stack (optimized for performance)
- Headings: Bold, larger size
- Body: Regular weight
- Monospace: Used for numeric values

### Spacing & Layout
- Border Radius: `0.75rem` (12px)
- Padding: Consistent 1rem (16px) spacing
- Gap: 0.75rem (12px) between elements

---

## Performance Considerations

1. **React.useCallback**: Memoized functions prevent unnecessary re-renders
2. **Efficient State Updates**: Minimal state changes for optimal performance
3. **CSS Transitions**: Hardware-accelerated animations
4. **Lazy Loading**: Components loaded on demand
5. **Tree Shaking**: Vite eliminates unused code
6. **TypeScript**: Compile-time optimization

---

## Educational Value

This project effectively demonstrates:

1. **Circular Queue Implementation**: Complete working example with all operations
2. **Pointer Management**: Front and rear pointer updates with modulo arithmetic
3. **State Transitions**: Traffic light state machine
4. **Overflow/Underflow Handling**: Proper error checking
5. **Real-World Application**: Traffic management use case
6. **User Interface Design**: Clean, intuitive controls
7. **Event-Driven Programming**: React hooks and effects
8. **Type Safety**: TypeScript benefits
9. **Component Architecture**: Modular design principles
10. **Animation & Feedback**: User experience enhancement

---

## Possible Extensions

1. **Multi-Lane Support**: Multiple queues for different lanes
2. **Priority Queue**: Emergency vehicles get priority
3. **Analytics Dashboard**: Statistics on throughput, wait times
4. **AI-Based Timing**: Adaptive signal timing based on queue length
5. **IoT Integration**: Connect to real traffic sensors
6. **Historical Data**: Store and visualize traffic patterns
7. **Multiple Intersections**: Network of traffic signals
8. **Pedestrian Signals**: Additional queue for pedestrian crossings
9. **Export Functionality**: Download operation logs as CSV
10. **Dark/Light Mode**: Theme toggle

---

## Testing Scenarios

### Test Case 1: Normal Operation
- **Steps**: Start simulation, observe automatic enqueue/dequeue
- **Expected**: Cars added during red, removed during green
- **Status**: ✓ Passed

### Test Case 2: Queue Full
- **Steps**: Fill queue to capacity, attempt enqueue
- **Expected**: Toast notification "Queue is full!"
- **Status**: ✓ Passed

### Test Case 3: Queue Empty
- **Steps**: Empty entire queue, attempt dequeue
- **Expected**: Toast notification "Queue is empty!"
- **Status**: ✓ Passed

### Test Case 4: Resize Queue
- **Steps**: Change queue size from 8 to 12
- **Expected**: Queue resets, new size applied
- **Status**: ✓ Passed

### Test Case 5: Speed Control
- **Steps**: Adjust speed slider from 1x to 2x
- **Expected**: Operations execute twice as fast
- **Status**: ✓ Passed

### Test Case 6: Manual Controls
- **Steps**: Use manual enqueue/dequeue buttons
- **Expected**: Operations execute immediately, logged correctly
- **Status**: ✓ Passed

---

## CONCLUSION

The **Traffic Signal Simulator** project successfully demonstrates the practical application of a **circular queue** data structure in a real-world traffic management scenario. Through this interactive web application, abstract data structure concepts become tangible and easy to understand.

### Key Achievements:

1. **Practical Implementation**: Successfully implemented all circular queue operations (enqueue, dequeue, overflow, underflow) with constant time complexity O(1).

2. **Real-World Connection**: Effectively bridges theoretical DSA concepts with urban traffic management, making learning more engaging and relevant.

3. **Visual Learning**: Provides clear visual feedback for every operation through animations, color-coded indicators, and real-time status updates.

4. **Educational Value**: Demonstrates FIFO (First-In-First-Out) principles, pointer management, modulo arithmetic for wrap-around, and state machines through traffic light cycles.

5. **Interactive Features**: Offers both automatic simulation and manual control, allowing users to experiment and understand queue behavior at their own pace.

6. **Modern Technology Stack**: Built using industry-standard tools (React, TypeScript, Tailwind CSS) ensuring maintainable, scalable, and performant code.

7. **Comprehensive Testing**: All operations tested successfully including normal flow, edge cases (overflow/underflow), dynamic resizing, and speed control.

### Learning Outcomes:

- Understanding of circular queue structure and its advantages over linear queues
- Mastery of pointer management and wrap-around logic using modulo operations
- Knowledge of time and space complexity analysis
- Experience with state management and event-driven programming
- Practical application of data structures in solving real-world problems

### Project Impact:

This simulator serves as an excellent educational tool for students learning data structures and algorithms. It transforms passive learning into active experimentation, allowing users to visualize how circular queues work in practice. The traffic signal metaphor makes the concept relatable and memorable.

### Future Scope:

The project foundation allows for several enhancements:
- Multi-lane support for multiple queues
- Priority queues for emergency vehicles
- Analytics dashboard for traffic patterns
- AI-based adaptive signal timing
- Integration with IoT sensors for real data

### Final Remarks:

The Traffic Signal Simulator successfully meets all project objectives by demonstrating core DSA concepts through an engaging, interactive, and visually appealing application. It proves that circular queues are not just theoretical constructs but practical solutions for real-world problems like traffic management, print job scheduling, and buffer management in computer systems.

The project showcases professional web development practices while maintaining educational focus, making it valuable both as a learning resource and as a demonstration of technical capabilities.

---

## References

1. React Documentation: https://react.dev/
2. TypeScript Handbook: https://www.typescriptlang.org/docs/
3. Tailwind CSS: https://tailwindcss.com/docs
4. Data Structures and Algorithms (Cormen, Leiserson, Rivest, Stein)
5. Circular Queue Concepts: GeeksforGeeks, TutorialsPoint
6. shadcn/ui Component Library: https://ui.shadcn.com/
7. Vite Build Tool: https://vitejs.dev/

---

**Project Repository**: Available on GitHub 
**Course**: Data Structures and Algorithms (ISWE102L)
