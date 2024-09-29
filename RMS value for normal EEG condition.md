clc;
clear all;
load('rc01_edfm.mat')
erp= val(1, 100:400)
eeg = val(1,:);
figure
subplot (2,1,1)
plot(erp)
title(' ERP Signal');
xlabel('Time');
ylabel('Amplitude');
subplot (2,1,2)
plot(eeg);
title('EEG Signal from ERP Data');
xlabel('Time');
ylabel('Amplitude');
 
 
alpha = bandpass(erp, [8 12], 130);
beta = bandpass(erp, [13 30], 130);
gamma = bandpass(erp, [30 100],130);
delta = bandpass(erp, [0.5 4], 130);
thetha= bandpass(erp, [4 8], 130);
 
figure
subplot(5,1,1)
plot(alpha)
title('Alpha Wave')
 
subplot(5,1,2)
plot(beta)
title('Beta Wave')
 
subplot(5,1,3)
plot(gamma)
title('Gamma Wave')
 
subplot(5,1,4)
plot(delta)
title('Delta Wave')
 
subplot(5,1,5)
plot(thetha)
title('Thetha Wave')
%rms value for beta wave
window_size = 40; 
overlap = 10; 
num_windows = floor((length(beta) - window_size) / overlap) + 1;
rms_values = zeros(1, num_windows);
for i = 1:num_windows
    start_idx = (i - 1) * overlap + 1;
    end_idx = start_idx + window_size - 1;
 window_data =beta(start_idx:end_idx);
rms_values(i) = rms(window_data);
end
figure;
plot(rms_values);
title('RMS Values with Sliding Window(epileptic)');
xlabel('Window Number');
ylabel('RMS Value');
fprintf('RMS Value: %f\n', rms_values)
 
%rms value for gamma wave
num_windows = floor((length(gamma) - window_size) / overlap) + 1;
rms_values = zeros(1, num_windows);
for i = 1:num_windows
   start_idx = (i - 1) * overlap + 1;
    end_idx = start_idx + window_size - 1;
 window_data =gamma(start_idx:end_idx);
rms_values(i) = rms(window_data);
end
figure;
plot(rms_values);
title('RMS Values with Sliding Window(epileptic)');
xlabel('Window Number');
ylabel('RMS Value');
fprintf('RMS Value: %f\n', rms_values)


