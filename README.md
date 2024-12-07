# renv2pak

**renv2pak** is a small web-based utility to help you install R packages defined in a `renv.lock` file using the [`pak`](https://pak.r-lib.org/) package. This tool can be used as a workaround when you encounter issues with `renv::restore()`, especially when migrating your environment to newer versions of R or dealing with complicated dependency resolutions.

**Link to the App:** [https://harshanal.github.io/renv2pak/](https://harshanal.github.io/renv2pak/)  

## Why This Tool?

When using `renv` for reproducible R environments, you typically rely on `renv::restore()` to set up your project dependencies exactly as defined in the `renv.lock` file. However, in some cases—such as after upgrading to a newer version of R or encountering tricky dependency installation problems—`renv::restore()` may fail, hang, or otherwise not behave as expected.

This is where **renv2pak** comes in. Instead of struggling with the restore process directly, you can:

1. Convert the `renv.lock` file into a `pak::pak()` installation command.
2. Run that command in your R environment.
3. Once the packages are installed, optionally run `renv::snapshot()` to capture the new environment state.

While this approach may not perfectly replicate every subtle nuance of `renv::restore()`, it can help you recover a functioning environment more quickly, and then get back to work.

## How It Works

1. **Paste `renv.lock`:** Copy the contents of your project's `renv.lock` file into the **renv2pak** web app.
2. **Choose Options:** Decide whether you want to include the exact package versions recorded in the lock file.
3. **Generate Command:** Click "Generate pak Command" to produce:
   - An `install.packages("pak")` command to ensure `pak` is available.
   - A `pak::pak(c(...))` command containing all your packages (and versions, if selected).
4. **Copy & Run:** Copy the generated command into your R session. This will install (or update) all the packages as per the `renv.lock` file.
5. **Snapshot (Optional):** If you want to maintain a reproducible state via `renv`, run `renv::snapshot()` to capture your newly installed packages in an updated lock file.

## Recommended Workflow

1. **Before Starting:** Ensure you have a backup of your original `renv.lock` file.
2. **Run renv2pak:**
   - Paste `renv.lock` content into the [renv2pak app](https://harshanal.github.io/renv2pak/).
   - If strict versions are desired, check the "Include package versions" box.
   - Generate the command.
3. **In R:**
   - Run the `install.packages("pak")` command (if `pak` is not already installed).
   - Run the `pak::pak(...)` command to install all the packages.
4. **Validate Installation:**
   - Check if your code runs as expected.
   - If everything is stable, run `renv::snapshot()` to capture the new state.
5. **Future Reproducibility:**
   - Your newly updated `renv.lock` file can now be used to restore environments in future sessions or by collaborators.

## Disclaimer

This approach is a workaround and might not adhere to strict reproducibility standards. It bypasses some of `renv`’s core functionalities. For stable, long-term reproducibility, continue to rely on `renv::restore()` whenever possible. Use **renv2pak** as a tool of last resort in tricky situations.

## Contributing and Feedback

Issues, suggestions, and improvements are welcome. Feel free to open a GitHub issue or submit a pull request to improve this project.
