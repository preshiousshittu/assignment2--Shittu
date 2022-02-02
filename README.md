# Precious Shittu
## NY Pizza Suprema
A neat **pizza** place in new york that is about a two minute walk form **madison square garden**. 
=================
# Section with an ordered list
Closet airport: LaGuardia Airport

1. get a taxi from the D terminal 

2. ask them to take you to **NY Pizza Suprema, 413 8th Ave, New York, NY 10001** the taxis have gps so it should take your there. the ride should be about 30 minutes

items you should try:
- their Buffelo Chicken pizza

- their round cheese pizza

- the grandma pizza




[About me page](AboutMe.md)

---
# Tables

| Name | Location | cost |
| ---  | ---------|------|
| gaming| pretty much anywhere| depends on the setup|
|digital art| mostly at home| you can get a drawing tablet for as cheap as 30 dollars
|Soccer | a nice field or any field really| it is pretty cheap all you need is a ball|
| Table tennis| a table tennis table| a cheap table could go for like 160 dollars

---
# Pithy Quotes
>The greatest glory in living lies not in never falling, but in rising every time we fall. -  *Nelson Mandela*

>The way to get started is to quit talking and begin doing. - *Walt Disney*
---
# Code Fencing 
> Reverse Polish notation (RPN), also known as reverse Łukasiewicz notation, Polish postfix notation or simply postfix notation, is a mathematical notation in which operators follow their operands, in contrast to Polish notation (PN), in which operators precede their operands. It does not need any parentheses as long as each operator has a fixed number of operands. The description "Polish" refers to the nationality of logician Jan Łukasiewicz,[1] who invented Polish notation in 1924. (https://en.wikipedia.org/wiki/Reverse_Polish_notation)

```
bool delim(char c) {
    return c == ' ';
}

bool is_op(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
}

int priority (char op) {
    if (op == '+' || op == '-')
        return 1;
    if (op == '*' || op == '/')
        return 2;
    return -1;
}

void process_op(stack<int>& st, char op) {
    int r = st.top(); st.pop();
    int l = st.top(); st.pop();
    switch (op) {
        case '+': st.push(l + r); break;
        case '-': st.push(l - r); break;
        case '*': st.push(l * r); break;
        case '/': st.push(l / r); break;
    }
}

int evaluate(string& s) {
    stack<int> st;
    stack<char> op;
    for (int i = 0; i < (int)s.size(); i++) {
        if (delim(s[i]))
            continue;

        if (s[i] == '(') {
            op.push('(');
        } else if (s[i] == ')') {
            while (op.top() != '(') {
                process_op(st, op.top());
                op.pop();
            }
            op.pop();
        } else if (is_op(s[i])) {
            char cur_op = s[i];
            while (!op.empty() && priority(op.top()) >= priority(cur_op)) {
                process_op(st, op.top());
                op.pop();
            }
            op.push(cur_op);
        } else {
            int number = 0;
            while (i < (int)s.size() && isalnum(s[i]))
                number = number * 10 + s[i++] - '0';
            --i;
            st.push(number);
        }
    }

    while (!op.empty()) {
        process_op(st, op.top());
        op.pop();
    }
    return st.top();
}

```
from here - https://cp-algorithms.com/string/expression_parsing.html

