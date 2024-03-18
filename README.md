# bajaj


const express = require('express');
const bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.json());

app.post('/bfhl', (req, res) => {
  const { array } = req.body;

  if (!Array.isArray(array)) {
    return res.status(400).json({
      is_success: false,
      error: 'Invalid input. Expected an array.'
    });
  }

  const evenNumbers = [];
  const oddNumbers = [];
  const alphabets = [];

  array.forEach(item => {
    if (typeof item === 'number') {
      if (item % 2 === 0) {
        evenNumbers.push(item);
      } else {
        oddNumbers.push(item);
      }
    } else if (typeof item === 'string') {
      if (/^[a-zA-Z]+$/.test(item)) {
        alphabets.push(item.toUpperCase());
      }
    }
  });

  const userId = `john_doe_${new Date().getFullYear()}`;

  res.status(200).json({
    is_success: true,
    user_id: userId,
    even_numbers: evenNumbers,
    odd_numbers: oddNumbers,
    alphabets: alphabets
  });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
