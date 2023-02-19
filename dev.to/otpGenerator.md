# Generate a Non Repetitive One Time Password (OTP) in Vanilla JS

&emsp; Have you wondered how to write a simple **JavaScript** (Vanilla JS) function to generate text or numbers? In this case, a JavaScript function that generates a nonrepetitive OTP. There might be libraries and frameworks for your backend services to make use of, for the functionality of verifying the users or similar. Yet, you can be asked in an interview to write a code for the same, or your project's bundle size might be a critical factor, so you might not be able to include a separate package just for generating text or numbers. So, let's discuss how to achieve the same via **Vanilla JS**.

## Code

```javascript
const generateOtp = (otpLength = 6) => {
  let otpCode = "";
  const possibleDigits = "0123456789";
  while (otpCode.length < otpLength) {
    let currentDigit = possibleDigits.charAt(
      Math.floor(Math.random() * possibleDigits.length)
    );
    if (!otpCode.includes(currentDigit)) {
      otpCode += currentDigit;
    }
  }
  return otpCode;
};

console.log(`Your OTP is ${generateOtp()}`); // As the function is called without any parameters, the default value of 6 will be considered as the length of the OTP

console.log(`Your OTP is ${generateOtp(4)}`); // For four digit OTP
```

Preview in [CodeSandBox](https://codesandbox.io/p/sandbox/romantic-mirzakhani-9lift1?file=%2Findex.js&selection=%5B%7B%22endColumn%22%3A45%2C%22endLineNumber%22%3A15%2C%22startColumn%22%3A45%2C%22startLineNumber%22%3A15%7D%5D)

## Explanation

- First, create a function named `generateOTP` and pass in a required parameter `otpLength`.
- A default value of 6 is assigned for OTP length if no parameter is passed.
- Declare a variable `otpCode` that will be returned when the function is called.
- Declare a variable `possibleDigits` that holds the digits/characters to be considered for generating the OTP.
- The `while` loop is executed until `otpCode.length` is less than `otpLength`. That is, the loop will execute till it generates the `otpLength` of numbers (in this case, its six digits)
- Within the loop, generate a random character from the `possibleDigits` string using `possibleDigits.charAt(Math.floor(Math.random() * possibleDigits.length))` and store the index in a temporary variable `currentDigit`
- Check if the generated character exists in `otpCode` using `if (!otpCode.includes(currentDigit))`.
- If it doesn't exist, add the generated character to the `otpCode` string using `otpCode += currentDigit`.
- The function returns the generated `OTP` using the `return otpCode` statement.;

## Output

<img src="https://i.postimg.cc/DwBxdHpK/image.png" />

&emsp;You can make use of such functions and make multiple generators for your use case, especially with the help of `regex` (regular expressions) to have ultimate customized generator functions without any 3rd party library. This approach helps you to understand the underlying concept and will help you to come up with similar solutions to similar questions in interviews, coding rounds, etc. when attending interviews.