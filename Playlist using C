#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <windows.h>

struct songs {
    struct songs *prev, *next;
    char song[20], type[20], artist[20];
    int dur;
};
typedef struct songs sgs;
sgs *head = NULL;

void addsong() {
    sgs *ptr = (sgs *)malloc(sizeof(sgs));
    if (!ptr) {
        printf("Memory overflow\n");
        return;
    }
    printf("Enter the song name, artist, song type, and duration of it\n");
    scanf("%s %s %s %d", ptr->song, ptr->artist, ptr->type, &ptr->dur);
    if (!head) {
        head = ptr;
        head->next = head;
        head->prev = head;
        printf("New song added\n");
        return;
    }
    sgs *last = head->prev;
    last->next = ptr;
    ptr->prev = last;
    ptr->next = head;
    head->prev = ptr;
    printf("New song added\n");
}

void delsong() {
    printf("Enter the song to delete\n");
    char key[20];
    scanf("%s", key);
    if (!head) {
        printf("No songs in the list\n");
        return;
    }
    sgs *ptr = head;
    do {
        if (strcmp(ptr->song, key) == 0) {
            if (ptr->next == ptr) {
                free(ptr);
                head = NULL;
            } else {
                ptr->prev->next = ptr->next;
                ptr->next->prev = ptr->prev;
                if (ptr == head) {
                    head = ptr->next;
                }
                free(ptr);
            }
            printf("Song deleted\n");
            return;
        }
        ptr = ptr->next;
    } while (ptr != head);
    printf("Song not found\n");
}

sgs* searchsong() {
    char key[20];
    printf("Enter the song you want to listen to\n");
    scanf("%s", key);
    if (!head) {
        printf("No song in list\n");
        return NULL;
    }
    sgs *ptr = head;
    do {
        if (strcmp(ptr->song, key) == 0) {
            printf("Current playing song is %s\n", key);
            return ptr;
        }
        ptr = ptr->next;
    } while (ptr != head);
    printf("Song not found\n");
    return NULL;
}

void playsong(sgs *curr_song) {
    sgs *temp = curr_song;
    int choice;
    while (1) {
        printf("Current playing song is %s\n", temp->song);
        Sleep(1000); // Uncomment if you want to add a delay
        printf("Enter 1 to continue, 2 to change song, 3 to stop: ");
        scanf("%d", &choice);
        if (choice == 2) {
            printf("Enter choice\n1)Previous\n2)Next song\n3)Search song\n");
            scanf("%d", &choice);
            switch (choice) {
                case 1:
                    temp = temp->prev;
                    break;
                case 2:
                    temp = temp->next;
                    break;
                case 3:
                    temp = searchsong();
                    if (!temp) {
                        temp = curr_song; // If search fails, continue with current song
                    }
                    break;
                default:
                    printf("Enter a valid choice\n");
                    break;
            }
        } else if (choice == 3) {
            break; // Stop playing
        } else {
            temp = temp->next;
        }
    }
}

void displaysongs() {
    if (!head) {
        printf("No songs in the list\n");
        return;
    }
    sgs *ptr = head;
    do {
        printf("Song name: %s\tArtist name: %s\tSong type: %s\tSong duration: %d\n",
               ptr->song, ptr->artist, ptr->type, ptr->dur);
        ptr = ptr->next;
    } while (ptr != head);
}

int main() {
    int choice;
    sgs *curr_song = head;
    while (1) {
        printf("Enter the choice\n1)Start playing songs\n2)Add song\n3)Delete song\n4)Change song\n5)Display songs\n6)Exit\n");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                if (head) {
                    playsong(head);
                } else {
                    printf("No songs to play\n");
                }
                break;
            case 2:
                addsong();
                break;
            case 3:
                delsong();
                break;
            case 4:
                if (curr_song) {
                    printf("Enter choice\n1)Previous\n2)Next song\n3)Search song\n");
                    scanf("%d", &choice);
                    switch (choice) {
                        case 1:
                            curr_song = curr_song->prev;
                            break;
                        case 2:
                            curr_song = curr_song->next;
                            break;
                        case 3:
                            curr_song = searchsong();
                            if (!curr_song) {
                                curr_song = head; // If search fails, fallback to the head
                            }
                            break;
                        default:
                            printf("Enter a valid choice\n");
                            break;
                    }
                } else {
                    printf("No song is currently playing\n");
                }
                break;
            case 5:
                displaysongs();
                break;
            case 6:
                exit(0);  // Make sure to properly terminate the main function
                break;
            default:
                printf("Enter a valid choice\n");
                break;
        }
    }
}
