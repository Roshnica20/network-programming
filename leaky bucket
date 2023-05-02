#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int bucket_size = 100;
int output_rate = 10;
int bucket_content = 0;
time_t last_check;

void tick() {
    time_t current_time = time(NULL);
    double time_elapsed = difftime(current_time, last_check);
    last_check = current_time;

    // calculate how much water has leaked from the bucket
    double leak_amount = time_elapsed * output_rate;
    bucket_content = bucket_content - (int)leak_amount;
    if (bucket_content < 0) {
        bucket_content = 0;
    }
}

int add(int packet_size) {
    tick();
    if (packet_size <= bucket_size - bucket_content) {
        bucket_content += packet_size;
        return 1;
    } else {
        return 0;
    }
}

int main() {
    last_check = time(NULL);

    // send 20 packets, each with size 8
    int i;
    for (i = 0; i < 20; i++) {
        if (add(8)) {
            printf("Packet sent successfully\n");
        } else {
            printf("Packet dropped\n");
        }
        sleep(100);
    }

    return 0;
}
