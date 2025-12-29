# Tactical-Deception-Decoy-Emitter
// DecoyEmitter.ts

interface Position {
    x: number;
    y: number;
}

class DecoyEmitter {
    private activeDecoys: Map<string, Position> = new Map();

    /**
     * Deploys a static decoy at a target location to distract enemies.
     * @param id Unique identifier for the decoy.
     * @param pos Coordinate where the decoy will appear.
     */
    public deployDecoy(id: string, pos: Position): void {
        console.log(`[DECEPTION] Deploying decoy ${id} at [${pos.x}, ${pos.y}]`);
        this.activeDecoys.set(id, pos);
        
        // In a real game engine, this would trigger a visual/radar entity.
    }

    /**
     * Checks if a decoy is currently active.
     */
    public isDecoyActive(id: string): boolean {
        return this.activeDecoys.has(id);
    }

    public removeDecoy(id: string): void {
        this.activeDecoys.delete(id);
        console.log(`[DECEPTION] Decoy ${id} expired or destroyed.`);
    }
}

// Example Usage
const emitter = new DecoyEmitter();
emitter.deployDecoy("Ghost_Alpha", { x: 45, y: 88 });
