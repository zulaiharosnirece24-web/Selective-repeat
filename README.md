#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#include <dos.h>   // for delay()

void main() {
    int i, j = 0, n, window = 4, lost;
    clrscr();
    randomize();

    printf("Enter total number of frames: ");
    scanf("%d", &n);

    while (j < n) {
        printf("\nSending frames: ");
        for (i = j + 1; i <= j + window && i <= n; i++)
            printf("%d ", i);

        delay(1000);

        // Randomly simulate frame loss (Selective Reject)
        lost = rand() % window;

        if (lost == 0) {
            printf("\nNo acknowledgement for frame %d", j + 1);
            printf("\nRetransmitting frame %d...", j + 1);
            delay(1000);
        } else {
            j += window;
            if (j > n)
                j = n;
            printf("\nAcknowledgement received up to frame %d", j);
        }
    }

    printf("\n\nAll frames sent successfully (Selective Repeat ARQ)\n");
    getch();
}
