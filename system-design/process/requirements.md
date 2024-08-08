# Handling Requirements

## Functional Requirements

The requirements that define what a system is supposed to do. They describe the various functions that the system must perform. Whats usually in the AC's.

- A user authentication system must validate user credentials and provide access levels.
- An e-commerce website should allow users to browse products, add them to a cart, and complete purchases.
- A report generation system must collect data, process it, and generate timely reports.

## Non-Functional Requirements

These requirements describe how the system performs a task, rather than what tasks it performs. They are related to the `quality` attributes of the system. Whats usually not in the AC's.

- `Scalability`: The system should handle growth in users or data.
- `Performance`: The system should process transactions within a specified time.
- `Availability`: The system should be up and running a defined percentage of time.
- `Security`: The system must protect sensitive data and resist unauthorized access.

## Usage and Decision Making in System Design

Mould the solution around the requirements.

### Clarify Requirements

Start by asking questions to understand both functional and non-functional requirements. Interviewers often leave these vague to see if you'll probe for more details.

### Prioritize

Not all requirements are equally important. Identify which ones are critical for the system’s success.

### Trade-offs

Discuss trade-offs related to different architectural decisions, especially concerning non-functional requirements. For example, a system highly optimized for read operations might have slower write operations.

### Use Real-World Examples

If you can, relate your points to real-world systems or your past experiences. This shows practical understanding.

### Balance

Ensure you're not focusing too much on one type of requirement over the other. A well-rounded approach is often necessary.
