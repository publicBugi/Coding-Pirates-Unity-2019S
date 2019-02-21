# Våben

## Opsætning af Våben

## Typer af våben


## Weapon Script
```C#
public float damage = 10f;
public float range = 100f;
public float impactForce = 10f;

public Camera fpsCam;

void Update()
{
    if(Input.GetButtonDown("Fire1")){
        Shoot();
    }
}

void Shoot(){
    
    RaycastHit hit;
    
    if(Physics.Raycast(fpsCam.transform.position, fpsCam.transform.forward, out hit, range)){

        Target target = hit.transform.GetComponent<Target>();
        if(target != null){
            target.TakeDamage(damage);
        }

        if(hit.rigidbody != null){
            hit.rigidbody.AddForce(-hit.normal * impactForce);
        }
    }
}
```

## Target Script
```C#
public float health = 50f;

public void TakeDamage(float amount){
    
    health -= amount;

    if(health <= 0){
        Destroy(gameObject);
    }
}
```