---
toc: True
comments: True
layout: notebook
title: Beneficial and Harmful Effects
courses: {'csp': {'week': 12, 'categories': ['4.A']}}
categories: ['C1.4']
---

## Programming effects
Programming, like any other field, has both beneficial and potentially harmful aspects. The more that programming advances, the more we have to discuss benefits and harmful effects that it brings to society.

## Example of Program with both benefitial and harmful effects


```python
    # Automated phone system of a customer service line for a major company
    def check_business_hours(hour):
        return 8 <= hour < 18

    def main():
        try:
            user_input = input("Please enter the current time (24-hour format, e.g., 14 for 2:00 PM): ")
            current_time = int(user_input)

            if check_business_hours(current_time):
                print("You are being connected to customer service.")
            else:
                print("Sorry, the business is closed at the moment. Please call back during business hours (8 am to 6 pm).")

        except ValueError:
            print("Invalid input. Please enter a valid 24-hour time.")

    if __name__ == "__main__":
        main()
```

    Sorry, the business is closed at the moment. Please call back during business hours (8 am to 6 pm).


## Beneficial effects: 
- It saves time for both parties as they limit the hours that a worker needs to answer calls for the company. 
- It checks whether the entered time is within the business hours (8 am to 6 pm). This ensures that customers are only connected to customer service during operational hours.
## Negative effects:
- The time may not be versatile for people in different time zones.  
- The system lacks customization options such as providing services available outside business hours such as offering automated assistance, or redirecting to online support resources.

## The benefits and harmful effects of a Multirotor
A multirotors also known as a drone, is a type of rotorcraft that has multiple rotors. Inventions such as these are the same as code and have harmful and beneficial effects.

Benefits: Deliveries, finding lost people, aereal photography is easy.
Harmful: Flying in unregulated zones is illegal and dangerous, privacy concerns.

## Popcorn Hack 1: Name one beneficial and harmful effect of a Wii controller. (hint: it can be a physical harmful effect)
Benefit: Entertain yourself

Effect: Hitting yourself in the head with the controller when you lose your grip

## Computing innovations can have impacts beyond their intended effects

## Example 1: The internet
The internet was originally created for scientists to easily share information remotely without needing to send or receive mail from one another. Nowadays, many people use the internet more than they sleep, as the internet has become an integral part of our lives in many ways. Think about how often you use social media, or do school assignments online, or send a simple email. Our use of the internet can cultivate dopamine feedback loops, such as when your crush likes your post on instagram, you get a snap back from that cute girl, or you find a funny TikTok that makes you laugh hysterically. These make us want to seek out these feelings more and more and experience those seconds of happiness. These effects of the internet lead to people having major issues like sleep deprivation, depression, and anxiety.

- Original Purpose:
    - Created for scientists to share information remotely.
    - Eliminated the need for physical mail in communication.
- Contemporary Usage:
    - Integral part of daily life.
    - Extensive use for social media, school assignments, emails.
- Impact on Well-being:
    - Potential for dopamine feedback loops.
    - Examples: Social media likes, Snapchat responses, TikTok enjoyment.
- Consequences:
    - Increased internet use may lead to sleep deprivation.
    - Associated with higher rates of depression and anxiety.

## Popcorn Hack 2: What 3 apps do you hae the most screentime on and how much are you on it? 

1: Safari Web Browser (5 hours per week)
2: Clock (10 minutes per week)
3: Apple News (5 minutes per week)

## Example 2: Microtransactions
Definition: a payment of very small value, especially for a special feature of a product such as a video game

- Original Purpose:
    - Free game access, purchase virtual extras.
- Usage:
    - Common in free-to-play games, revenue for developers.
- Deviation:
    - Pay-to-Win, aggressive tactics, loot boxes.
    - Microtransactions may reduce ads but imply paywalls.
- Concerns:
    - Debates on industry impact, ethics.
    - Mixed player views: support vs. criticism.
- Ongoing:
    - Continuous industry debates.

## Example 3: Artificial Intelligence

### What is AI?

Artificial Intelligence (AI) is about making computers do tasks that typically require human intelligence, like learning, problem-solving, and understanding language.

### Beneficial Effects of AI:

1. **Automation and Efficiency:**
   - AI helps with repetitive tasks, making things faster and freeing up time for more interesting work.

2. **Medical Advancements:**
   - AI assists in medical tasks, improving diagnosis, treatment plans, and drug discovery.

3. **Enhanced Customer Experience:**
   - AI-powered chatbots provide quick and personalized customer support.

4. **Innovations in Education:**
   - AI creates personalized learning experiences for students.

5. **Predictive Analytics:**
   - AI analyzes data to make predictions, helping businesses make better decisions.

### Harmful Effects of AI:

1. **Job Displacement:**
   - Automation by AI can lead to job loss in some industries.

2. **Bias and Fairness Issues:**
   - AI systems might have biases, causing unfair outcomes.

3. **Privacy Concerns:**
   - AI use in surveillance raises concerns about privacy.

4. **Autonomous Weapons:**
   - AI-powered weapons raise ethical questions about their use in warfare.

5. **Dependency on Technology:**
   - Relying too much on AI may lead to a loss of human skills and critical thinking.

## Homework Hack: Come up with a Program with a beneficial and harmful effects. (You don't have to code it, but your ideas has to be detailed and organized)

Program: An economic optimizer algorithm intended to ensure total sustainability for a country and its constituency. Such an apparatus would fully automatically delegate labor and resources to civic uses in order to ensure maximum quality of life for all members of its creator's society. While such large-scale automation is not currently possible, increasing complexity of neural networks and increasing predictive capability of physical models may make steps toward it feasible in the next several decades.

Benefits:
- Reliance on work as a means of survival is eliminated.
- Humans will have generally more free time to dedicate to artistic or scientific pursuits.
- Optimal solutions will be found to most practical civic issues without the possibility of human error or corruption.

Problems:
- The needs of the majority may result in diminished quality of life for minority elements if resources are limited (though this depends on how the algorithm behaves).
- Systemically biased or corrupted datasets may result in inappropriate behavior.
- A society dependent on robust automation is likely to unlearn maintenance skills and subsequently collapse when the systems break down after inevitable degradation over long timescales.
