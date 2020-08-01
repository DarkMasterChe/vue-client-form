h2 {
    margin-left: 50px;
}

.left {
  margin-right: 330px;
}

select {
  width: 150px;
  padding: 5px 35px 5px 5px;
  font-size: 14px;
  width: 440px;
  height: 50px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background:  #c5baba;
  border-radius: 4px;
}

.right-row {
  margin-left: 20px;
}

.selector {
  margin-top: -10px;
  width: 450px;
  height: 80px;
  border: 2px solid #c5baba;
  border-radius: 4px;
} 

.adress-container {
    width: 1000px;
    max-width: 100%;
    margin: 20px auto 25px auto;
}

.styled-input-ad {
    width: 220px;
    margin: 5px;
    position: relative;
    border-radius: 4px;
    float: left;
    max-width: 100%;
    margin-left: 70px;
}

.wide { 
   float: left;
    width: 400px;
    max-width: 100%;
}

.styled-input label {
    color: rgb(27, 26, 26);
    padding: 10px 10px 10px 10px;
    position: absolute;
    top: 10px;
    left: 0;
    -webkit-transition: all 0.25s ease;
    transition: all 0.25s ease;
    pointer-events: none;
}

input:focus ~ span {
    width: 100%;
    -webkit-transition: all 0.075s ease;
    transition: all 0.075s ease;
}

input {
    padding: 20px;
    border: 10px;
    width: 100%;
    font-size: 15px;
    background-color: #c5baba;
    color: rgb(32, 32, 32);
    border-radius: 4px;
}

.styled-input.wide { 
   float: left;
    width: 400px;
    max-width: 100%;
}

input:focus ~ label, input:valid ~ label {
    margin-left: 12px;
    font-size: 12px;
    color: rgb(24, 23, 23);
    top: -5px;
    -webkit-transition: all 0.225s ease;
    transition: all 0.225s ease;
}