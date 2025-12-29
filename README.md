# Tactical-Deception-Decoy-Emitter
// DecoyEmitter.ts

interface Position {
    x: number;
    y: number;
}

// DecoyEmitter.ts (Updated Implementation)

interface Position {
    x: number;
    y: number;
}

class DecoyEmitter {
    private activeDecoys: Map<string, Position> = new Map();
    // NEW: Store movement vectors for "Dynamic Decoys"
    private decoyVectors: Map<string, { dx: number, dy: number }> = new Map();

    public deployDecoy(id: string, pos: Position, movementVector?: { dx: number, dy: number }): void {
        this.activeDecoys.set(id, pos);
        
        // NEW EDIT: If a vector is provided, make the decoy "move"
        if (movementVector) {
            this.decoyVectors.set(id, movementVector);
            console.log(`[DECEPTION] Deploying DYNAMIC decoy ${id} with movement mimicry.`);
        } else {
            console.log(`[DECEPTION] Deploying static decoy ${id}.`);
        }
    }

    /**
     * NEW: Simulates a movement tick for all active dynamic decoys.
     * This makes decoys look like real players on the enemy radar.
     */
    public updateDecoyPositions(): void {
        this.activeDecoys.forEach((pos, id) => {
            const vector = this.decoyVectors.get(id);
            if (vector) {
                const newPos = {
                    x: pos.x + vector.dx,
                    y: pos.y + vector.dy
                };
                this.activeDecoys.set(id, newPos);
                console.log(`[SYNC] Decoy ${id} moved to [${newPos.x.toFixed(1)}, ${newPos.y.toFixed(1)}]`);
            }
        });
    }

    public removeDecoy(id: string): void {
        this.activeDecoys.delete(id);
        this.decoyVectors.delete(id);
        console.log(`[DECEPTION] Decoy ${id} removed.`);
    }
}

// Example Usage
const emitter = new DecoyEmitter();
// Deploy a decoy that moves slowly to the right
emitter.deployDecoy("Ghost_Beta", { x: 10, y: 10 }, { dx: 1.5, dy: 0 });

// Simulate game ticks
emitter.updateDecoyPositions();
emitter.updateDecoyPositions();
