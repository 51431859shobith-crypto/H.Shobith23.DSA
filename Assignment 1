#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Tab {
    int pageID;
    char url[100];
    struct Tab *prev;
    struct Tab *next;
};

struct Tab *current = NULL;
int pageCounter = 1;

void visitNewPage() {
    struct Tab *newTab = (struct Tab*)malloc(sizeof(struct Tab));
    newTab->pageID = pageCounter++;
    printf("Enter URL: ");
    scanf("%s", newTab->url);
    newTab->prev = current;
    newTab->next = NULL;

    if (current != NULL) {
        current->next = newTab;
    }
    current = newTab;

    printf("Now viewing: [%d] %s\n", current->pageID, current->url);
}

void goBack() {
    if (current != NULL && current->prev != NULL) {
        current = current->prev;
        printf("Moved back to: [%d] %s\n", current->pageID, current->url);
    } else {
        printf("No previous tab.\n");
    }
}

void goForward() {
    if (current != NULL && current->next != NULL) {
        current = current->next;
        printf("Moved forward to: [%d] %s\n", current->pageID, current->url);
    } else {
        printf("No next tab.\n");
    }
}

void showCurrentTab() {
    if (current != NULL) {
        printf("Current tab: [%d] %s\n", current->pageID, current->url);
    } else {
        printf("No tab open.\n");
    }
}

void closeCurrentTab() {
    if (current == NULL) {
        printf("No tab to close.\n");
        return;
    }

    struct Tab *temp = current;

    if (current->prev != NULL) {
        current->prev->next = current->next;
    }
    if (current->next != NULL) {
        current->next->prev = current->prev;
    }

    if (current->next != NULL) {
        current = current->next;
    } else {
        current = current->prev;
    }

    printf("Closed tab: [%d] %s\n", temp->pageID, temp->url);
    free(temp);
}

void showHistory() {
    struct Tab *temp = current;
    while (temp != NULL && temp->prev != NULL) {
        temp = temp->prev;
    }
    if (temp == NULL) {
        printf("No history.\n");
        return;
    }
    printf("Browser History:\n");
    while (temp != NULL) {
        printf("[%d] %s\n", temp->pageID, temp->url);
        temp = temp->next;
    }
}

int main() {
    int choice;

    while (1) {
        printf("\n===== Browser Menu =====\n");
        printf("1. Visit a new page\n");
        printf("2. Go back\n");
        printf("3. Go forward\n");
        printf("4. Show current tab\n");
        printf("5. Close current tab\n");
        printf("6. Show history\n");
        printf("7. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: visitNewPage(); break;
            case 2: goBack(); break;
            case 3: goForward(); break;
            case 4: showCurrentTab(); break;
            case 5: closeCurrentTab(); break;
            case 6: showHistory(); break;
            case 7: printf("Exiting...\n"); return 0;
            default: printf("Invalid choice.\n");
        }
    }

    return 0;
}
