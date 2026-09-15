# Design-of-FIR-Filters-using-Hamming-window
#          DESIGN OF FIR DIGITAL FILTERS USING HAMMING WINDOW
# AIM: 
          
  To generate design of FIR digital filters using Hamming Window using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM for LPF,HPF,BPF, BSF
LPF
```clc;
clear;
close;

// FIR LOW PASS FILTER USING HAMMING WINDOW
// Symmetry condition: h(-n) = h(n)

// Input
N = evstr(input("Enter number of samples N: ", "string"));
wc_pi = evstr(input("Enter cutoff frequency (Wc/pi): ", "string"));

// Cutoff frequency
Wc = wc_pi * %pi;

// Symmetric sample index
n = -(N-1)/2 : (N-1)/2;

// Initialize
hd = zeros(1,N);

// Ideal Low Pass Filter
for k = 1:N

    if n(k) == 0 then
        hd(k) = Wc/%pi;
    else
        hd(k) = sin(Wc*n(k))/(%pi*n(k));
    end

end

// Hamming Window
w = 0.54 + 0.46*cos(2*%pi*n/(N-1));

// FIR coefficients
h = hd .* w;

// Display
disp("Sample index n:");
disp(n);

disp("Ideal impulse response hd(n):");
disp(hd);

disp("Hamming Window w(n):");
disp(w);

disp("FIR LOW PASS FILTER COEFFICIENTS:");
disp(h);

// Check symmetry
disp("Symmetry check h(-n) = h(n):");
disp(h == h($:-1:1));

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR Low Pass Filter - Hamming Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m)*exp(-%i*omega(k)*n(m));
    end
end

subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("Frequency Response");
```
HPF
```
clc;
clear;
close;

// FIR HIGH PASS FILTER USING HAMMING WINDOW

// Input
N = evstr(input("Enter number of samples N: ", "string"));
wc_pi = evstr(input("Enter cutoff frequency (Wc/pi): ", "string"));

// Convert cutoff frequency to radians
Wc = wc_pi * %pi;

// Sample index
n = 0:N-1;

// Alpha
alpha = (N-1)/2;

// Initialize ideal impulse response
hd = zeros(1,N);

// Ideal High Pass Filter
for k = 1:N
    
    x = n(k) - alpha;
    
    if x == 0 then
        hd(k) = 1 - Wc/%pi;
    else
        hd(k) = (sin(%pi*x) - sin(Wc*x)) / (%pi*x);
    end
    
end

// Hamming Window
w = 0.54 - 0.46*cos(2*%pi*n/(N-1));

// FIR filter coefficients
h = hd .* w;

// Display results
disp("Hamming Window:");
disp(w);

disp("FIR HIGH PASS FILTER COEFFICIENTS:");
disp(h);

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR High Pass Filter - Hamming Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m)*exp(-%i*omega(k)*n(m));
    end
end

// Magnitude response
subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR High Pass Filter using Hamming Window");
```
BPF
```
clc;
clear;
close;

// FIR BAND PASS FILTER USING HAMMING WINDOW
// Symmetry condition: h(-n) = h(n)

// Input
N = evstr(input("Enter number of samples N: ", "string"));

wc1_pi = evstr(input("Enter lower cutoff frequency (Wc1/pi): ", "string"));

wc2_pi = evstr(input("Enter upper cutoff frequency (Wc2/pi): ", "string"));

// Cutoff frequencies
Wc1 = wc1_pi * %pi;
Wc2 = wc2_pi * %pi;

// Symmetric sample index
n = -(N-1)/2 : (N-1)/2;

// Initialize
hd = zeros(1,N);

// Ideal Band Pass Filter
for k = 1:N

    if n(k) == 0 then
        hd(k) = (Wc2-Wc1)/%pi;
    else
        hd(k) = (sin(Wc2*n(k))-sin(Wc1*n(k))) / ...
                (%pi*n(k));
    end

end

// Hamming Window
w = 0.54 + 0.46*cos(2*%pi*n/(N-1));

// FIR coefficients
h = hd .* w;

// Display
disp("Sample index n:");
disp(n);

disp("Ideal impulse response hd(n):");
disp(hd);

disp("Hamming Window w(n):");
disp(w);

disp("FIR BAND PASS FILTER COEFFICIENTS:");
disp(h);

// Symmetry check
disp("Symmetry check h(-n) = h(n):");
disp(h == h($:-1:1));

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR Band Pass Filter - Hamming Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m)*exp(-%i*omega(k)*n(m));
    end
end

subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR Band Pass Filter - Frequency Response");
```
BSP
```
clc;
clear;
close;

// FIR BAND STOP FILTER USING HAMMING WINDOW
// Symmetry condition: h(-n) = h(n)

// Input
N = evstr(input("Enter number of samples N: ", "string"));

wc1_pi = evstr(input("Enter lower cutoff frequency (Wc1/pi): ", "string"));

wc2_pi = evstr(input("Enter upper cutoff frequency (Wc2/pi): ", "string"));

// Convert cutoff frequencies
Wc1 = wc1_pi * %pi;
Wc2 = wc2_pi * %pi;

// Symmetric sample index
n = -(N-1)/2 : (N-1)/2;

// Initialize
hd = zeros(1,N);

// Ideal Band Stop Filter
for k = 1:N

    if n(k) == 0 then
        hd(k) = 1 - (Wc2-Wc1)/%pi;
    else
        hd(k) = (sin(Wc1*n(k))-sin(Wc2*n(k))) / ...
                (%pi*n(k));
    end

end

// Hamming Window
w = 0.54 + 0.46*cos(2*%pi*n/(N-1));

// FIR coefficients
h = hd .* w;

// Display
disp("Sample index n:");
disp(n);

disp("Ideal impulse response hd(n):");
disp(hd);

disp("Hamming Window w(n):");
disp(w);

disp("FIR BAND STOP FILTER COEFFICIENTS:");
disp(h);

// Symmetry check
disp("Symmetry check h(-n) = h(n):");
disp(h == h($:-1:1));

// Impulse response
subplot(2,1,1);
plot2d3(n,h);
xlabel("n");
ylabel("h(n)");
title("FIR Band Stop Filter - Hamming Window");

// Frequency response
M = 500;
omega = linspace(0,%pi,M);
H = zeros(1,M);

for k = 1:M
    for m = 1:N
        H(k) = H(k) + h(m)*exp(-%i*omega(k)*n(m));
    end
end

subplot(2,1,2);
plot(omega,abs(H));
xlabel("Frequency (rad/sample)");
ylabel("Magnitude");
title("FIR Band Stop Filter - Frequency Response");
```

# OUTPUT for LPF,HPF,BPF, BSF
LPS
<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/88601ff0-2f90-4a2e-b109-ee2a3bd52363" />
HPS
<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/1509ef1e-dd93-4c63-98f7-ffa63424545f" />
BPS
<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/87ba96f3-85fe-404b-a57c-e33ed86c7955" />
BSF
<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/c9386045-e2ab-4845-8e89-cd9da1701920" />


# RESULT
Thus,the FIR digital filter using hamming window is successfully verified
