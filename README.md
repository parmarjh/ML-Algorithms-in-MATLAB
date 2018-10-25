# 1. Linear Regression #

A restaurant franchise is considering different cities for opening a new outlet. The chain already has trucks in various cities and we have data for profits and populations from the cities. 

Lets use this data to determine which city to expand to next outlet. The first column is the population of a city and the second column is the profit of a food truck in that city. A negative value for profit indicates a loss.

Here, Linear Regression with one variable is Implemented to predict profits for a food truck in new outlet. 

### Plotting the Data

```matlab
function plotData(x, y)
%PLOTDATA Plots the data points x and y into a new figure 
%   PLOTDATA(x,y) plots the data points and gives the figure axes labels of
%   population and profit.

figure; % open a new figure window

%               Plot the training data into a figure using the 
%               "figure" and "plot" commands. Set the axes labels using
%               the "xlabel" and "ylabel" commands. Assume the 
%               population and revenue data have been passed in
%               as the x and y arguments of this function.
%
%   can use the 'rx' option with plot to have the markers
%       appear as red crosses. Furthermore, you can make the
%       markers larger by using plot(..., 'rx', 'MarkerSize', 10);


data = load('ex1data1.txt'); % read comma separated data
x = data(:, 1); y = data(:, 2);
m = length(y);

plot(x, y, 'rx', 'MarkerSize', 10); % Plot the data
ylabel('Profit in $10,000s'); % Set the y??axis label
xlabel('Population of City in 10,000s'); % Set the x??axis label
end
```
<p align="center">
    <img src="https://github.com/AdroitAnandAI/ML-Algorithms-in-MATLAB/blob/master/1.%20Linear%20Regression/images/1.2.1.PNG">
</p>

### Gradient Descent ###

Here, we fit the Linear Regression parameters to our dataset using Gradient Descent.

![2.2.1](https://github.com/AdroitAnandAI/ML-Algorithms-in-MATLAB/blob/master/1.%20Linear%20Regression/images/2.2.1.PNG)

Lets perform gradient descent to minimize the cost function, it is helpful to monitor the convergence by computing the cost.

```matlab
function J = computeCost(X, y, theta)
%COMPUTECOST Compute cost for linear regression
%   J = COMPUTECOST(X, y, theta) computes the cost of using theta as the
%   parameter for linear regression to fit the data points in X and y

% Initialize some useful values
m = length(y); % number of training examples

J = 0;

% Compute the cost of a particular choice of theta and set to J
J = sum((X*theta- y).^2)/(2*m);
end
```

Next, we will implement gradient descent. Here, we minimize the value of the cost function by changing the values of the vector 'theta'. A good way to verify that gradient descent is working correctly is to look at the value of cost function and check that it is decreasing with each step.

```matlab
function [theta, J_history] = gradientDescent(X, y, theta, alpha, num_iters)
%GRADIENTDESCENT Performs gradient descent to learn theta
%   theta = GRADIENTDESCENT(X, y, theta, alpha, num_iters) updates theta by 
%   taking num_iters gradient steps with learning rate alpha

% Initialize some useful values
m = length(y); % number of training examples
J_history = zeros(num_iters, 1);

for iter = 1:num_iters

    %  Perform a single gradient step on the parameter vector
    %               theta. 
    %
    %  While debugging, it can be useful to print out the values
    %       of the cost function (computeCost) and gradient here.
    %

    %%This is non vectorized implementation of gradient descent
%     a = theta(1) - X(:,1)'*(X*theta- y)*(alpha/m);
%     b = theta(2) - X(:,2)'*(X*theta- y)*(alpha/m);
%     theta(1) = a;
%     theta(2) = b;
    
    %%This is vectorized implementation of gradient descent
    theta = theta - X'*(X*theta- y)*(alpha/m);
    
    % Save the cost J in every iteration    
    J_history(iter) = computeCost(X, y, theta);
    %%fprintf('With theta = [0 ; 0]\nCost computed = %f\n', J_history(iter));

end

end
```

<p align="center">
    <img src="https://github.com/AdroitAnandAI/ML-Algorithms-in-MATLAB/blob/master/1.%20Linear%20Regression/images/2.2.4.PNG">
</p>
