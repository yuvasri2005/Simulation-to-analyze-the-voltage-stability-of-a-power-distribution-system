# Simulation-to-analyze-the-voltage-stability-of-a-power-distribution-system
## AIM
To Simulate and analyze the voltage stability of a power distribution system

## APPARATUS REQUIRED
•	MATLAB

## MATLAB CODING

% Voltage Stability Analysis of a Power Distribution System

% Displays 4 graphs in one figure using subplots

clc; clear; close all;

% System Parameters

V_s = 1.0; % Sending end voltage (p.u.)

X = 0.5; % Line reactance (p.u.)

P_load = linspace(0, 2, 50); % Real power demand (p.u.)

pf = 0.9; % Power factor (lagging)

% Initialize storage

V_r = zeros(size(P_load));

Q_load = zeros(size(P_load));

PF_array = zeros(size(P_load));

% Voltage stability analysis

for k = 1:length(P_load)

 P = P_load(k);
 
 % Reactive power (Q = P * tan(phi))
 
 phi = acos(pf);
 
 Q = P * tan(phi);
 
 Q_load(k) = Q;
 
 % Approximate quadratic relation for receiving end voltage
 
 a = 1;
 
 b = (P*X);
 
 c = -(V_s^2);

 Vr_sq = (-b + sqrt(b^2 - 4*a*c)) / (2*a);

 if Vr_sq > 0
 
 V_r(k) = sqrt(Vr_sq);
 
 else
 
 V_r(k) = NaN;
 
 end

 % Power factor
 
 S = sqrt(P^2 + Q^2);
 
 PF_array(k) = P / S;
 
end

% -------------------------------

% Plot all 4 graphs in one figure

figure;

subplot(2,2,1);


plot(P_load, V_r, 'b-o','LineWidth',1.5);

xlabel('Active Power P (p.u.)'); ylabel('Voltage V_r (p.u.)');

title('P–V Curve'); grid on;

subplot(2,2,2);

plot(Q_load, V_r, 'r-s','LineWidth',1.5);

xlabel('Reactive Power Q (p.u.)'); ylabel('Voltage V_r (p.u.)');

title('Q–V Curve'); grid on;

subplot(2,2,3);

plot(V_r, PF_array, 'g-^','LineWidth',1.5);

xlabel('Voltage V_r (p.u.)'); ylabel('Power Factor');

title('Power Factor vs Voltage'); grid on;

subplot(2,2,4);

plot(P_load, Q_load, 'm-d','LineWidth',1.5);

xlabel('Active Power P (p.u.)'); ylabel('Reactive Power Q (p.u.)');

title('P–Q Relationship'); grid on;

sgtitle('Voltage Stability Analysis - Distribution System');


## OUTPUT

<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/ea981253-6675-4fce-af2f-74133e232505" />

## RESULT

The P–V and Q–V curves show that increasing load reduces receiving-end voltage, leading to instability beyond a critical limit.
Hence, the system has a limited voltage stability margin, and excess load may cause voltage collapse.
