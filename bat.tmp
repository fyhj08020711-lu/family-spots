@echo off
cd /d "%~dp0"
set GH_USER=fyhj08020711-lu
set REPO=family-spots
set URL=https://github.com/%GH_USER%/%REPO%.git

where gh >nul 2>nul
if %errorlevel%==0 (
  gh repo view %GH_USER%/%REPO% >nul 2>nul
  if errorlevel 1 gh repo create %GH_USER%/%REPO% --public
)

if not exist .git git init
git branch -M main
git config user.name "%GH_USER%"
git config user.email "%GH_USER%@users.noreply.github.com"
git remote set-url origin %URL% 2>nul || git remote add origin %URL%
git fetch origin main 2>nul && git reset --soft origin/main
git add -A
git commit -m "update"
git push -u origin main
if errorlevel 1 (
  echo.
  echo Push failed. If the repo does not exist yet, create it first:
  echo   https://github.com/new?name=%REPO%   ^(Public, no README^)
  echo then double-click this file again.
  pause
  exit /b 1
)

where gh >nul 2>nul
if %errorlevel%==0 gh api -X POST repos/%GH_USER%/%REPO%/pages -f "source[branch]=main" -f "source[path]=/" >nul 2>nul

echo.
echo Done. Site: https://%GH_USER%.github.io/%REPO%/
echo ^(first time Pages needs ~1 minute. If 404: repo Settings - Pages - Deploy from branch main / root^)
pause
